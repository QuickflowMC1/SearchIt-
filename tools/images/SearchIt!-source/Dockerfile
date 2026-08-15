ARG VERSION

FROM uazo/chromium:$VERSION

ARG SearchIt_SHA
ENV SearchIt_SHA=$SearchIt_SHA

ARG HTTP_PROXY
ENV HTTP_PROXY=$HTTP_PROXY
ENV HTTPS_PROXY=$HTTP_PROXY
ENV https_proxy=$HTTP_PROXY

#USER lg
WORKDIR /home/lg/working_dir

RUN sudo chown lg /etc/apt/apt.conf.d/proxy.conf
RUN sudo echo "Acquire::http::Proxy \"$HTTP_PROXY\";" >/etc/apt/apt.conf.d/proxy.conf
RUN sudo apt-get update

COPY apply-SearchIt!-patches.sh .

RUN sudo chmod +x ./apply-SearchIt!-patches.sh && \
    mkdir SearchIt! && \
    cd SearchIt! && \
    git init && \
    git remote add origin https://github.com/uazo/SearchIt! && \
    git fetch origin $SearchIt_SHA && \
    git reset --hard FETCH_HEAD && \
    cd ..

RUN ./apply-SearchIt!-patches.sh

