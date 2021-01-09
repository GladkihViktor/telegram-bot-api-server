FROM ubuntu:20.04
ENV TZ=Europe/Moscow
ENV TELEGRAM_PORT 8081

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt update
RUN apt upgrade -y
RUN apt install -y git
RUN apt install -y make git zlib1g-dev libssl-dev gperf cmake clang-10 libc++-dev libc++abi-dev

RUN git clone --recursive https://github.com/tdlib/telegram-bot-api.git
RUN cd telegram-bot-api \
    && rm -rf build && mkdir build \
    && cd ./build && CXXFLAGS="-stdlib=libc++" CC=/usr/bin/clang-10 CXX=/usr/bin/clang++-10 \
     cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=.. .. \
    && cmake --build . --target install && cd ../.. \
    && ls -l telegram-bot-api/bin/telegram-bot-api*


WORKDIR  /telegram-bot-api/build/
RUN ln -sf /dev/stdout ./telegrambot.log
