# Use my nightly automated container builds of the dev.go2go branch as the base.
# Add some basic shell tooling.
FROM mrothy/go2go:latest
RUN apk add --no-cache \
    git \
    bash \
    zsh

# https://github.com/golang/go/issues/39619

RUN GO111MODULE=on go get -v \
    golang.org/x/tools/gopls@dev.go2go \
    golang.org/x/tools@dev.go2go

# To get IDE support in VSCode, we need a prerelease extension. Since
# it is not published in marketplace, we download it manually into the
# home directory so that it's easy to install.
#
# Unfortunately, `code --install-extension` does not seem to work within the
# devcontainer shell, so on first launch we need to manually install from UI:
#
# Extensions > Install from VSIX...
RUN cd /root && \
    wget https://github.com/golang/vscode-go/releases/download/20200722/go2go-0.0.0.vsix
