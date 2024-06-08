# Deep Linking with Jetpack Compose in Android

This repository demonstrates the implementation of deep linking in an Android application using Jetpack Compose and Kotlin. With this functionality, users can enter the app through links entered in their browser.

## Features

- **Deep Linking**: Seamlessly navigate to specific parts of the app using browser links.
- **Jetpack Compose**: Utilizes Jetpack Compose for modern, declarative UI design.
- **Kotlin**: Written entirely in Kotlin, leveraging its powerful features for Android development.


## Screenshots

<div style="display: flex; justify-content: center; align-items: center;">
    <img src="https://github.com/Bhavyansh03-tech/DeepLinking/assets/96388594/fdd29ba7-a7d4-418e-86f7-14ad2d0b6630" alt="Web Browser" style="width: 200px; height: auto; margin-right: 10px;">
    <img src="https://github.com/Bhavyansh03-tech/DeepLinking/assets/96388594/f706a057-5275-418e-95b6-183c322cb6de" alt="Application" style="width: 200px; height: auto;">
</div>


## Getting Started

### Installation

1. **Clone the repository**:
    ```sh
    git clone https://github.com/Bhavyansh03-tech/DeepLinking.git
    ```
2. **Open the project in Android Studio**:
    - File > Open > Select the cloned project directory.

3. **Build the project**:
    - Ensure that the necessary dependencies are downloaded and configured by building the project via Build > Make Project.

### Usage

1. **Define Deep Links**:
    - Deep links are defined in the `AndroidManifest.xml` file under the activity declaration or through `Tools>ApplicationLinkAssistance>Create or add Link to it and then Test it`.
    ```xml
    <activity
            android:name=".MainActivity"
            android:exported="true"
            android:theme="@style/Theme.DeepLinking">
            <tools:validation testUrl="https://www.xiver.com" />

            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
            <intent-filter android:autoVerify="true">
                <action android:name="android.intent.action.VIEW" />

                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />

                <data android:scheme="https" />
                <data android:host="www.xiver.com" />
            </intent-filter>
        </activity>
    ```

2. **Handle Deep Links in Compose**:
    - Use `NavHost` and `NavController` to handle navigation in Jetpack Compose based on the deep link.

    ```kotlin
    class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            DeepLinkingTheme {
                val navController = rememberNavController()

                val uri = "https://www.xiver.com"

                NavHost(
                    navController = navController,
                    startDestination = "home"
                ){

                    composable(
                        route = "home",
                        deepLinks = listOf(
                            navDeepLink {
                                uriPattern = "$uri/{id}"
                            }
                        )
                    ){ backStackEntry ->
                        val id = backStackEntry.arguments?.getString("id")

                        Box(
                            modifier = Modifier.fillMaxSize(),
                            contentAlignment = Alignment.Center
                        ){
                            Text(text = id ?: "No id passed")
                        }
                    }

                }
            }
        }
    }
}
    ```

3. **Testing Deep Links**:
    - Open a browser and enter the URL that matches the deep link pattern defined in the manifest (e.g., `https://www.example.com/path?id=123`).

### Project Structure

- `MainActivity.kt`: The main entry point of the app.
- `navigation/`: Contains navigation logic using Jetpack Compose.
- `ui/`: Contains the composable functions and UI components.

## Contributing

Contributions are welcome! Please fork the repository and use a feature branch. Pull requests are warmly welcome.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a pull request

## Acknowledgements

- Inspiration from various Android development tutorials and documentation.


## Contact

For questions or feedback, please contact [@Bhavyansh03-tech](https://github.com/Bhavyansh03-tech).
