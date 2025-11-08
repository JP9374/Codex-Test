# California Weather Grafana Dashboard

This repository contains a ready-to-import Grafana dashboard that highlights real-time weather insights for key California cities. The dashboard uses free public APIs for temperature, humidity, and forecast data so you can keep an eye on coastal and inland conditions at a glance.

## Features

- **Los Angeles temperature trend** sourced from the Open-Meteo hourly forecast.
- **San Francisco temperature trend** to compare coastal swings with Southern California.
- **Sacramento relative humidity stat** that surfaces the latest inland moisture level.
- **Los Angeles forecast table** with narrative details from the National Weather Service.
- Auto-refreshes every 30 minutes and is ready for dark-theme displays.

## Prerequisites

1. Grafana 9.0+ (open source or Grafana Cloud).
2. The [JSON API data source plugin](https://grafana.com/grafana/plugins/marcusolsson-json-datasource/) installed and enabled in your Grafana instance.
3. Outbound internet access from Grafana so it can call the Open-Meteo and National Weather Service APIs.

## Importing the Dashboard

1. Install the JSON API plugin if it is not already available.
2. Create a new data source of type **JSON API** and set the **UID** to `json-api` (or update the dashboard import to match your chosen UID).
3. In Grafana, choose **Dashboards → New → Import**.
4. Upload [`grafana/california-weather-dashboard.json`](grafana/california-weather-dashboard.json) or paste its raw JSON.
5. When prompted, map the `JSON API` input to the data source you created and click **Import**.

You should now see the dashboard with four panels that begin populating after the first API calls. Use Grafana's time picker to widen or narrow the analysis window.

## Customization Tips

- Adjust the latitude/longitude query parameters in the Open-Meteo URLs to track additional California cities.
- Duplicate the humidity stat panel to visualize wind speeds, precipitation, or other Open-Meteo metrics by updating the `hourly` query string.
- The forecast table currently targets the Los Angeles (LOX) grid point from the National Weather Service. Replace the `gridpoints/LOX/153,44` segment with another California office and grid coordinate pair for localized forecasts.
- Modify the dashboard refresh interval if you need faster or slower updates depending on API rate limits.

## Data Source Notes

- Open-Meteo returns metric units by default. Convert to Fahrenheit inside Grafana using field transformations if desired.
- National Weather Service APIs enforce rate limiting; Grafana handles HTTP caching but consider staggering refresh intervals if you add more panels hitting the same endpoint.
- All APIs used here are public and do not require authentication, making this dashboard simple to deploy for demos or status monitors.

## License

This project is provided under the MIT License. Feel free to adapt it for your own monitoring needs.
