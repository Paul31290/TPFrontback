<template>
<body onload="fetchCountries()">    
    <h2>Villes dans chaque pays</h2>
        <div class="form-group">
        </div>
        <div>
            <hr>
        </div>
<body>    
</template>

<script setup>
    import { reactive, onMounted } from "vue";
// @ is an alias to /src


const data = reactive({
  allCities: [],
  allCountries: [],
});

function fetchCities() {
  // Utilise l'API ad-hoc pour avoir le pays de chaque ville
    var citiesHref = document.getElementById("countrySelector").value;
        fetch(citiesHref)
            then(response => response.json())
            .then(json => showTemplate("citiesTemplate", json._embedded, "cities"))
            .catch(error => showError(error));
}

// Utilise l'API REST auto-générée pour avoir les pays
function fetchCountries() {
  fetch("api/countries")
    .then((response) => response.json())
    .then((json) => {
      data.allCountries = json._embedded.countries;
    })
    .catch((error) => alert(error));
}
function showCountrySelector(resultJson) {
            showTemplate("countriesTemplate", resultJson._embedded, "countries");
            // On montre les villes pour le premier pays
            showCities();
        }
</script>


