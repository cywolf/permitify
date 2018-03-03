FROM python-libindy:latest

ENV HOME=/app
WORKDIR $HOME
USER root

# needed for external dependencies
RUN apk add --no-cache git

ARG wallet_path=$HOME/.indy_client/wallet
ADD ./docker/docker-entrypoint.sh /usr/local/bin/enter

RUN mkdir -p "$wallet_path" && \
    chown -R indy:0 $HOME /usr/local/bin "$wallet_path" \
    && chmod -R ug+rwx $HOME /usr/local/bin "$wallet_path"

USER indy

COPY ./src/requirements.txt $HOME/
RUN source $BUILD/bin/activate && \
    pip install -r requirements.txt

ADD ./src $HOME
ADD ./site_templates $HOME/site_templates

ENTRYPOINT ["sh", "/usr/local/bin/enter"]
