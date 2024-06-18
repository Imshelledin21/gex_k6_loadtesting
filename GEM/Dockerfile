# docker buildx build --platform linux/amd64 . -t basvdl/k6-custom
# docker push basvdl/k6-custom
FROM golang:1.17

RUN go install go.k6.io/xk6/cmd/xk6@latest

RUN git clone https://github.com/grafana/xk6-loki

WORKDIR "xk6-loki"

RUN xk6 build \
    --replace "github.com/mingrammer/flog=github.com/chaudum/flog@v0.4.4-0.20211115125504-92153be038e6" \
    --with "github.com/grafana/xk6-loki=$(pwd)" \
    --with "github.com/grafana/xk6-client-prometheus-remote@latest"

RUN mkdir /modules

RUN curl -o /modules/httpx.js https://jslib.k6.io/httpx/0.0.6/index.js

RUN curl -o /modules/k6-utils.js https://jslib.k6.io/k6-utils/1.1.0/index.js

RUN curl -o /modules/k6chaijs.js  https://jslib.k6.io/k6chaijs/4.3.4.1/index.js

ENTRYPOINT ["./k6"]