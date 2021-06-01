# Rzero-Android-SDK

### Integration using Gradle
```groovy
rootProject.allprojects {
    repositories {
       ...
       maven {
            name = "GitHubPackages"
            url = uri("https://maven.pkg.github.com/rzero-co/android-sdk")
            credentials {
                username = "rzero_sdk_user"
                password = "{YOUR_ACCESS_TOKEN_HERE}"
            }
        }
        ...
    }
}

dependencies {
        ...
        implementation ("co:rzero:${version-number}")
        ...
}
```

### Initialization

In Application.onCreate() or as early on in the app lifecycle, use the rzero.Builder to create an instance.  The parameters can be found in the rZero Customer Portal
```kotlin
class RZeroExampleApp : Application() {

    override fun onCreate() {
        super.onCreate()
        rzero.Builder(applicationContext)
                .isStaging(true)
                .clientId({YOUR_CLIENT_ID})
                .clientToken({YOUR_MOBILE_TOKEN})
                .activityLifecycleListenerOn(false) //When manually creating page_load/page_leave events/ for non native android mobile integrations set this to false
                .build()
    }
}
```

### Before e-commerce purchase (* required)
```kotlin
rzero.getInstance().flush()
```

### Set User id (* required)
```kotlin
rzero.getInstance().setUserId("{ID}")
```

### Log screen changes ( only needed when not using activityLifecycleListener - for non native integrations)
#### page_load (generic name) a.k.a logViewAppear (Android specific name) event when a view/screen appears (onResume)
```kotlin
rzero.getInstance().sendEventForVisibilityChange("{SCREEN_NAME}", true)
```
#### page_leave (generic name) a.k.a logViewDisappear (Android specific name) event when a view/screen disappears (onPause)
```kotlin
rzero.getInstance().sendEventForVisibilityChange("{SCREEN_NAME}", false)
```

### Implement EditTextWatcher for textfields - note- any field notated as password will receive '*' obfuscated text.
```kotlin
rzero.getInstance().addEditTextWatcher(this, R.id.name)

//Alternatively, you could send a list of ids
val viewIds = listOf(R.id.email, R.id.password)
rzero.getInstance().addEditTextWatcher(this, viewIds)
```

### Send custom events
```kotlin
rzero.getInstance().logCustomEvent(mapOf("event_name" to "login_screen", "key_1" to "value_1"))
```

### Console output
Send these Job uuids to let us verify the correctness of your integration.
```bash
ROLogUtil: rZero POSTED job uuid:db17602f-f448-4dcc-a557-ea9114a198ac	OK:true
ROLogUtil: rZero POSTED job uuid:3ae63a51-dfd7-45f0-8399-fc853d194bcd	OK:true
ROLogUtil: rZero POSTED job uuid:6dcc4caa-1209-43e7-a439-9349be342f54	OK:true
ROLogUtil: rZero POSTED job uuid:025f7e82-a920-4c54-beca-9bcb1ac32867	OK:true
```
