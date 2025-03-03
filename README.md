# CSIECouncil

此為台灣大學資訊工程系系學會專題訪談網站，含括歷年來各教授的採訪內容。

## Usage

1. Remove Ruby, bundler, gem installed currently
*Maybe* rvm might not work well if the system one is already installed.

3. Install rvm
See [Installing RVM](https://rvm.io/rvm/install)

**Remember to install GPG key.**

3. Install OpenSSL 1.1.1
Since the ruby version required is too old to support major versions recently. We have to install one manually.

For ubuntu, this might be helpful:
[How to install OpenSSL 1.1.1 and libSSL package?](https://askubuntu.com/questions/1126893/how-to-install-openssl-1-1-1-and-libssl-package)

5. Setup env vars
```bash
export warnflags=-Wno-error=implicit-function-declaration
export optflags="-w"

# This depends on your installation
MY_OPENSSL=$HOME/.openssl/openssl-1.1.1g
MY_OPENSSL=/opt/homebrew/Cellar/openssl@1.1/1.1.1w

export PKG_CONFIG_PATH=$MY_OPENSSL/lib/pkgconfig
```

6. Install ruby
```bash
rvm get master

rvm reinstall 2.7.0 --with-openssl="$MY_OPENSSL"
```

7. Install jekyll and bundler
```bash
gem install jekyll -- --with-openssl-dir="$MY_OPENSSL"
gem install bundler -v 2.3.16 -- --with-openssl-dir="$MY_OPENSSL"
```

8. Install required packages
```bash
bundle install                          
```

9. Local preview
```bash
bundle exec jekyll serve --livereload -- --with-openssl-dir="$MY_OPENSSL"
```

9. Reinstall `eventmachine` if something went wrong
```bash
gem uninstall eventmachine
gem install eventmachine -v 1.2.7 -- --with-openssl-dir="$MY_OPENSSL"
```

10. Build the site
```bash
bundle exec jekyll build --config _config_prod.yml -- --with-openssl-dir="$MY_OPENSSL"
```

The HTML files are stored in `_site/`.
