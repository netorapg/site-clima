<template>
    <div class="weather-container">
        <h2>Previsão do tempo</h2>
        <input type="text" v-model="city" placeholder="Digite o nome da cidade">
        <button @click="getWeatherData">Pesquisar</button>
        <div v-if="loading">
            <div class="loading-container">
                <div class="loading-spinner"></div>
            </div>
        </div>
        <div v-else-if="weatherData">
            <p class="temperature">Temperatura: {{ weatherData.current.temp_c }} °C</p>
            <p class="condition">Condição: {{ weatherData.current.condition.text }}</p>
        </div>
        <div v-else>
            <p>Insira o nome da cidade acima e clique em "Pesquisar" para obter a previsão do tempo.</p>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            city: '',
            weatherData: null,
            loading: false
        };
    },
    methods: {
        async getWeatherData() {
            if (this.city.trim() === '') {
                alert('Por favor, insira o nome da cidade.');
                return;
            }

            this.loading = true;
            this.weatherData = null; // Reset weatherData to null when starting a new request

            try {
                const response = await axios.get(`https://api.weatherapi.com/v1/current.json?key=ae6a3841e92a471a8bb171209242405&query=${this.city}`);
                this.weatherData = response.data;
            } catch (error) {
                console.error('Erro ao obter dados da API:', error);
            } finally {
                this.loading = false;
            }
        }
    }
};
</script>

<style>
.weather-container {
    font-family: Arial, sans-serif;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 20px;
    margin: 20px auto;
    max-width: 400px;
    text-align: center;
    background-color: #f9f9f9;
}

.temperature {
    font-size: 18px;
    margin-bottom: 10px;
}

.condition {
    font-size: 16px;
}

.loading-container {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 10px;
}

.loading-spinner {
    border: 4px solid rgba(0, 0, 0, 0.1);
    border-left-color: #333;
    border-radius: 50%;
    width: 24px;
    height: 24px;
    animation: spin 1s linear infinite;
}

@keyframes spin {
    to {
        transform: rotate(360deg);
    }
}

.input-container {
    margin-bottom: 10px;
}

input[type="text"],
button {
    padding: 8px;
    font-size: 16px;
}

button {
    cursor: pointer;
}
</style>
