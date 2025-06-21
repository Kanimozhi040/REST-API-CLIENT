package WeatherApi;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Scanner;
import org.json.JSONArray;
import org.json.JSONObject;

public class WeatherApiClient {

    // Fetch weather data as raw JSON string
    public static String fetchWeather(String city) {
        StringBuilder response = new StringBuilder();
        try {
            String urlString = "https://wttr.in/" + city + "?format=j1";
            URL url = new URL(urlString);
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");

            BufferedReader reader = new BufferedReader(
                new InputStreamReader(conn.getInputStream())
            );

            String line;
            while ((line = reader.readLine()) != null) {
                response.append(line);
            }
            reader.close();
        } catch (Exception e) {
            System.out.println("Error fetching data: " + e.getMessage());
        }

        return response.toString();
    }

    // Display weather information from JSON
    public static void displayWeather(String jsonData) {
        try {
            JSONObject obj = new JSONObject(jsonData);
            JSONArray weatherArray = obj.getJSONArray("weather");
            JSONObject weather = weatherArray.getJSONObject(0);

            String date = weather.getString("date");
            String maxTemp = weather.getString("maxtempC");
            String minTemp = weather.getString("mintempC");

            JSONObject hourly = weather.getJSONArray("hourly").getJSONObject(0);
            String condition = hourly
                .getJSONArray("weatherDesc")
                .getJSONObject(0)
                .getString("value");

            System.out.println("----------- Weather Report -----------");
            System.out.println("Date        : " + date);
            System.out.println("Condition   : " + condition);
            System.out.println("Max Temp    : " + maxTemp + " °C");
            System.out.println("Min Temp    : " + minTemp + " °C");
            System.out.println("--------------------------------------");

        } catch (Exception e) {
            System.out.println("Error parsing JSON: " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a city name: ");
        String city = scanner.nextLine();

        String jsonData = fetchWeather(city);

        if (!jsonData.isEmpty()) {
            displayWeather(jsonData);
        } else {
            System.out.println("No weather data received.");
        }

        scanner.close();
    }
}
