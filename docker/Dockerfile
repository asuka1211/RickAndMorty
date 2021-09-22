FROM gradle:7.2.0-jdk11

# Переменные с локальными путями для Android SDK и версиями инструментов
ENV SDK_URL="https://dl.google.com/android/repository/commandlinetools-linux-7583922_latest.zip" \
    ANDROID_HOME="/usr/local/android-sdk" \
    ANDROID_VERSION=30 \
    ANDROID_BUILD_TOOL_VERSION=30.0.2

# Скачиваем Android SDK, распаковываем и ставим + принимаем лицензии
RUN mkdir "$ANDROID_HOME" .android \
    && cd "$ANDROID_HOME" \
    && curl -o android-commandline-tools.zip $SDK_URL \
    && mkdir -p ${ANDROID_HOME}/cmdline-tools \
    && unzip -q android-commandline-tools.zip -d /tmp/ \
    && mv /tmp/cmdline-tools/ ${ANDROID_HOME}/cmdline-tools/latest \
    && rm android-commandline-tools.zip && ls -la ${ANDROID_HOME}/cmdline-tools/latest/

ENV PATH ${PATH}:${ANDROID_HOME}/cmdline-tools/tools/bin:${ANDROID_HOME}/cmdline-tools/latest/bin

RUN yes | sdkmanager --licenses

# Обновляем и устанавливаем инструментарий
RUN yes | sdkmanager --update
RUN yes | sdkmanager "emulator" "platform-tools" \
    "platforms;android-${ANDROID_VERSION}" \
    "build-tools;${ANDROID_BUILD_TOOL_VERSION}"
