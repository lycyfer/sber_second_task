<script lang="ts">
  let baseCurrency = "USD";
  let targetCurrency = "EUR";
  let baseAmount = 1;
  let targetAmount = 0;
  let rates = {};

  const fetchRates = async () => {
    try {
      const response = await fetch(
        `https://api.exchangerate-api.com/v4/latest/${baseCurrency}`
      );
      if (!response.ok) {
        throw new Error("Network response was not ok");
      }
      const data = await response.json();
      rates = data.rates;
      convert();
    } catch (error) {
      console.error("There was a problem with fetch operation:", error);
    }
  };

  const convert = () => {
    targetAmount = baseAmount * rates[targetCurrency];
  };

  fetchRates();
</script>

<main>
  <div>
    <select bind:value={baseCurrency} on:change={fetchRates}>
      <option value="USD">USD</option>
      <option value="EUR">EUR</option>
      <option value="USD">USD</option>
      <option value="EUR">EUR</option>
      <option value="AED">AED</option>
      <option value="ARS">ARS</option>
      <option value="AUD">AUD</option>
      <option value="CAD">CAD</option>
      <option value="CHF">CHF</option>
      <option value="CLP">CLP</option>
      <option value="CNY">CNY</option>
      <option value="GBP">GBP</option>
      <option value="HKD">HKD</option>
      <option value="RUB">RUB</option>
    </select>
    <input type="number" bind:value={baseAmount} on:input={convert} />

    <select bind:value={targetCurrency} on:change={convert}>
      <option value="USD">USD</option>
      <option value="EUR">EUR</option>
      <option value="AED">AED</option>
      <option value="ARS">ARS</option>
      <option value="AUD">AUD</option>
      <option value="CAD">CAD</option>
      <option value="CHF">CHF</option>
      <option value="CLP">CLP</option>
      <option value="CNY">CNY</option>
      <option value="GBP">GBP</option>
      <option value="HKD">HKD</option>
      <option value="RUB">RUB</option>
    </select>
    <input type="number" value={targetAmount} readonly />
  </div>
</main>
