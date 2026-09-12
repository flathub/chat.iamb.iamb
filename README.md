# Flatpak for [the iamb Matrix client](https://github.com/ulyssa/iamb)

## To update:

- Clone the iamb repo and checkout desired version
  ```sh
  git clone https://github.com/ulyssa/iamb
  git -C iamb switch --detach v0.0.12
  ```

- Use [flatpak-cargo-generator.py](https://github.com/flatpak/flatpak-builder-tools/tree/master/cargo)
  to generate `cargo-sources.json` from `iamb/Cargo.lock`:
  ```sh
  python flatpak-cargo-generator.py iamb/Cargo.lock -o cargo-sources.json
  ```

- Change SHA for the iamb source code in `chat.iamb.iamb.yml` to the release version

- Make sure you have the bits for building:
  ```sh
  flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
  flatpak install flathub org.freedesktop.Sdk//26.08
  flatpak install flathub org.freedesktop.Platform//26.08 
  flatpak install flathub org.freedesktop.Sdk.Extension.rust-stable/x86_64/26.08
  ```

- Build and locally install the flatpak:
  ```
  flatpak-builder build-dir chat.iamb.iamb.yml --user --install --force-clean --ccache
  ```
