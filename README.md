# Publishing plugin from gradle

## Intent

This plugin extends the project in order to fetch the wanted credentials from Hashicorp vault. As you can see it in the code base, this plugin is tiny and does one thing only.


It exposes a simple extension to your project so you can use it.


## Usage

```
buildscript {
  repositories {
    mavenCentra()
  }
  dependencies {
    classpath 'io.errorlab.gradle:vault:0.0.+'
  }
}
```

Make sure that you have `VAULT_ADDR` and `VAULT_TOKEN` defined when using gradle. After which, you have access to any credential with the following directives
```
project.vault.get("secret/my_secret")
```


example for Android:
```
$> vault write secret/android-signing-key-credentials key_password=12345 store_password=abcde
```
```
  signingConfigs {
    release {
      keyAlias 'release'
      keyPassword project.vault.get("secret/signing-keys")['data']['key_password']
      storeFile file('release.keystore')
      storePassword project.vault.get("secret/signing-keys")['data']['store_password']
    }
```


thats it.

All PR, comments and issues are welcome.
