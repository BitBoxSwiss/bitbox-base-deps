# bitbox-base-deps
This is a temporary repository to host binary dependencies for the [BitBox Base](https://github.com/digitalbitbox/bitbox-base) project, built for Linux ARMv8 cpu architecture, also known as aarch64 or arm64.

The binaries have been build on a RockPro64 board using Armbian 4.15.0.

## electrs

Electrum Server in Rust, used to serve Electrum wallet clients.
<https://github.com/romanz/electrs>

Reason for not using official binaries: no binary releases available.

Build it yourself (as root user):
```
# install Rust
mkdir rust
cd rust
curl https://static.rust-lang.org/dist/rust-1.39.0-aarch64-unknown-linux-gnu.tar.gz -o rust.tar.gz

# must return 'rust.tar.gz: OK'
echo "e27dc8112fe577012bd88f30e7c92dffd8c796478ce386c49465c03b6db8209f rust.tar.gz" | sha256sum -c -

tar --strip-components 1 -xzf rust.tar.gz
./install.sh

# install dependencies
apt install git clang cmake

# compile electrs
git clone https://github.com/romanz/electrs
cd electrs
git checkout tags/v0.8.0
git status
cargo build --release

# install electrs
cp ./target/release/electrs /usr/bin/
```
