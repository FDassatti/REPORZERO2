# Rzero-Android-SDK

### Integration using Gradle
```
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

In Application.onCreate() or as early on in the app lifecycle, use the rzero.Builder to create an instance.
```
public class RZeroExampleApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        new rzero.Builder(getApplicationContext())
                .isStaging(true)
                .clientId({YOUR_CLIENT_ID})
                .clientToken({YOUR_TOKEN})
                .build();

    }
}
```

### Set User id
```
 rzero.getInstance().setUserId((ID))
```

### Implement EditTextWatcher for textfields - note- any field notated as password will receive '*' obfuscated text.
```
rzero.getInstance().addEditTextWatcher(this, R.id.name);

//Alternatively, you could send a list of ids
List<Integer> viewIds = Arrays.asList(R.id.email, R.id.password);
rzero.getInstance().addEditTextWatcher(this, viewIds);
```

### Before e-commerce purchase
```
rzero.getInstance().flush()
```

### Send custom events
```
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
