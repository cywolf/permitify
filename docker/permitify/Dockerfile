FROM python-libindy:latest

WORKDIR $HOME
USER root

# needed for external dependencies
RUN apk add --no-cache git

ARG wallet_path=$BUILD/.indy_client/wallet
ADD ./docker/docker-entrypoint.sh /usr/local/bin/enter

RUN mkdir -p "${wallet_path}" && \
    chown -R indy:0 $HOME /usr/local/bin "${wallet_path}" \
    && chmod -R ug+rwx $HOME /usr/local/bin "${wallet_path}"

USER indy

COPY ./src/requirements.txt $HOME/
RUN source $BUILD/bin/activate && \
    pip --no-cache-dir install -r requirements.txt

ADD ./src $HOME
ADD ./site_templates $HOME/site_templates

ENV INDY_GENESIS_PATH $BUILD/.genesis

ENTRYPOINT ["sh", "/usr/local/bin/enter"]
