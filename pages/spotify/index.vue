<template>
  <section id="spotify">
    <div v-if="!isLoggedInToSpotify">
      <button
        @click="checkAndFetchToken"
        class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded"
      >
        Login with Spotify
      </button>
    </div>
    <!-- <div v-if="isLoggedInToSpotify">
      <button
        @click="logout"
        class="bg-red-500 hover:bg-red-600 text-white font-bold py-2 px-4 rounded mt-4"
      >
        Logout
      </button>
    </div> -->
    <div v-if="loading">Logging in...</div>
    <div v-if="error">{{ error }}</div>
    <div v-if="topArtists.length > 0">
      <h2 class="text-lg font-bold">Your Top Artists:</h2>
      <ul class="list-disc pl-5 mt-5">
        <li
          v-for="artist in topArtists"
          :key="artist.id"
          class="flex items-center mb-5"
        >
          <img
            v-if="artist.images.length"
            :src="artist.images[0].url"
            :alt="artist.name"
            class="rounded-full w-10 h-10 mr-2"
          />
          <strong>{{ artist.name }}</strong>
          <span class="ml-2 text-blue-500"
            >({{ artist.genres.join(", ") || "No genres listed" }})</span
          >
        </li>
      </ul>
      <div v-if="genreCount">
        <h2 class="text-lg font-bold mt-10">Genres Count:</h2>
        <ul class="list-disc pl-5">
          <li v-for="(count, genre) in genreCount" :key="genre">
            <strong>{{ genre }}:</strong> {{ count }} artist{{
              count > 1 ? "s" : ""
            }}
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, ref } from "vue";

// Configuration values
const clientID = "8e1a60c15f01436c8774da8c6b599e5b";
const clientSecret = "95f7c86e257247c7a59abda6b20f1434";
const redirectURI = "http://localhost:3000/spotify";
const state = "34fFs29kd09"; // Random string to prevent CSRF

// Reactive variables
const isLoggedInToSpotify = ref(false);
const loading = ref(false);
const error = ref(null);
const accessToken = ref(null);
const topArtists = ref([]);
const genreCount = ref({}); // To store genre counts

// Helper function to fetch access token
const getAccessToken = async (code) => {
  try {
    const response = await fetch("https://accounts.spotify.com/api/token", {
      method: "POST",
      headers: {
        "Content-Type": "application/x-www-form-urlencoded",
        Authorization: `Basic ${btoa(`${clientID}:${clientSecret}`)}`,
      },
      body: new URLSearchParams({
        grant_type: "authorization_code",
        code: code,
        redirect_uri: redirectURI,
      }),
    });

    const data = await response.json();

    if (response.ok) {
      const expiresIn = data.expires_in; // The access token expires in 3600 seconds (1 hour)
      const expirationTime = Date.now() + expiresIn * 1000; // Set expiration time
      localStorage.setItem("access_token", data.access_token);
      localStorage.setItem("token_expiration", expirationTime);
      accessToken.value = data.access_token;
      fetchTopArtists(data.access_token); // Fetch user's top artists
    } else {
      error.value = data.error || "Failed to fetch access token.";
    }
  } catch (e) {
    error.value = "An error occurred while fetching the access token.";
  } finally {
    loading.value = false;
    isLoggedInToSpotify.value = true;
  }
};

// Fetch top artists using the access token
const fetchTopArtists = async (token) => {
  try {
    const response = await fetch("https://api.spotify.com/v1/me/top/artists", {
      method: "GET",
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });

    const data = await response.json();

    if (response.ok) {
      topArtists.value = data.items;
      calculateGenreCount();
    } else {
      error.value = data.error || "Failed to fetch top artists.";
    }
  } catch (e) {
    error.value = "An error occurred while fetching top artists.";
  }
};

// Calculate genre counts
const calculateGenreCount = () => {
  const genres = {}; // Object to hold genre counts

  topArtists.value.forEach((artist) => {
    artist.genres.forEach((genre) => {
      // If genre already exists, increment the count, otherwise initialize it
      genres[genre] = genres[genre] ? genres[genre] + 1 : 1;
    });
  });

  genreCount.value = genres; // Store the genre count object
};

// Check if token is expired and return it or get a new one
const checkAndFetchToken = async () => {
  const storedToken = localStorage.getItem("access_token");
  const expirationTime = localStorage.getItem("token_expiration");

  // If token is valid and not expired, use it
  if (storedToken && expirationTime && Date.now() < expirationTime) {
    accessToken.value = storedToken;
    isLoggedInToSpotify.value = true;
    fetchTopArtists(storedToken);
  } else {
    // If token is expired or not found, get a new one
    const urlParams = new URLSearchParams(window.location.search);
    const code = urlParams.get("code");
    const returnedState = urlParams.get("state");

    if (!code) {
      // If there's no code or state doesn't match, redirect to Spotify login
      window.location.href =
        "https://accounts.spotify.com/authorize?" +
        new URLSearchParams({
          client_id: clientID,
          response_type: "code",
          redirect_uri: redirectURI,
          scope: "user-read-private user-read-email user-top-read", // Added `user-top-read` scope
          state: state,
          show_dialog: true, // Always show the Spotify login screen
        });
    } else {
      loading.value = true;
      getAccessToken(code); // Exchange code for access token
    }
  }
};
// Logout functionality to clear token and reset state
const logout = () => {
  // Clear the stored token and expiration time
  localStorage.removeItem("access_token");
  localStorage.removeItem("token_expiration");
  accessToken.value = null;
  isLoggedInToSpotify.value = false;
  topArtists.value = [];
  genreCount.value = {};
  window.location.href = "/spotify";
};

onMounted(() => {
  const urlParams = new URLSearchParams(window.location.search);
  const code = urlParams.get("code");
  const returnedState = urlParams.get("state");

  if (code && returnedState === state) {
    // If there is a code in the URL and it matches the state, fetch the token
    loading.value = true;
    getAccessToken(code); // Exchange code for access token
  } else {
    // Check the stored token for auto-login
    const storedToken = localStorage.getItem("access_token");
    const expirationTime = localStorage.getItem("token_expiration");

    if (storedToken && expirationTime && Date.now() < expirationTime) {
      isLoggedInToSpotify.value = true;
      accessToken.value = storedToken;
      fetchTopArtists(storedToken);
    } else {
      isLoggedInToSpotify.value = false;
    }
  }
});
</script>
