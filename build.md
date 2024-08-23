# Install ruby
brew install ruby

# Install rbenv and ruby-build
brew install rbenv

# Set up rbenv integration with your shell
rbenv init

# rbenv 2.7,1
rbenv install 2.7.1
rbenv global 2.7.1

# mac more than 10.14
sudo gem install bundler
sudo gem install -n /usr/local/bin/ jekyll