# EMQX Dashboard - RCE

This is a malicious plugin for [EMQX Dashboard](https://github.com/emqx/emqx-dashboard) which allows to execute commands remotely.

The code in this repository is mostly based on one of the latest releases of the [EMQX plugin template](https://github.com/emqx/emqx-plugin-template) repository.


----------------------

## Plugin Compilation

1. Install all the necessary dependencies, Erlang and rebar3. In the latest Kali release (Kali 2024.4) you can use:

```shell
sudo apt update
sudo apt install -y build-essential autoconf libncurses5-dev libssl-dev \
    libwxgtk3.2-dev libgl1-mesa-dev libglu1-mesa-dev libpng-dev \
    libssh-dev unixodbc-dev cmake
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.13.1
echo '. "$HOME/.asdf/asdf.sh"' >> ~/.bashrc
echo '. "$HOME/.asdf/completions/asdf.bash"' >> ~/.bashrc
source ~/.bashrc
asdf --version
asdf plugin-add erlang https://github.com/asdf-vm/asdf-erlang.git
asdf install erlang 25.3
asdf global erlang 25.3
wget https://s3.amazonaws.com/rebar3/rebar3
chmod +x rebar3
sudo mv rebar3 /usr/local/bin/
```

2. Create the necessary directory and clone the plugin repository:

```shell
mkdir -p ~/.config/rebar3/templates/emqx-plugin-template
git clone https://github.com/ricardojoserf/emqx-RCE ~/.config/rebar3/templates/emqx-plugin-template
```

3. (Optional) Modify the command to be executed by updating line 47 in "src/emqx_plugin_template.erl":

![img](https://raw.githubusercontent.com/ricardojoserf/ricardojoserf.github.io/refs/heads/master/images/emqx/Screenshot_1.png)

4. Generate the plugin as a tar.gz file:

```shell
rebar3 new emqx-plugin my_emqx_plugin
make -C my_emqx_plugin rel
cp my_emqx_plugin/_build/default/emqx_plugrel/my_emqx_plugin-1.0.0.tar.gz . 
```

5. Install and run via the EMQX Dashboard under the "Plugin" section.

----------------------

## Disclosure

Following discussions with the EMQX security team, they do not consider this a vulnerability but a "feature" and have no objections to this repository being public.

However, versions 5.8.6 and higher will mitigate this feature by not using default credentials and disabling the plugin installation from the dashboard (it will only be available through the CLI).
