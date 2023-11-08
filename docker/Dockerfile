FROM ubuntu:22.04

ARG USERNAME=docker
ARG USER_GID=1000
ARG USER_UID=1001

ENV NODE_VERSION 20

RUN apt update -y && apt upgrade -y 
RUN apt install -y sudo ca-certificates curl gnupg
RUN curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
RUN echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_VERSION.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list
RUN apt update && apt install -y vim nodejs
RUN npm i -g @nestjs/cli
RUN apt install -y git bash-completion

# Create user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME

# Switch to the new user
USER $USERNAME

# Create a global .gitconfig file with your Git configuration
RUN echo "[safe]" >> /home/$USERNAME/.gitconfig
RUN echo "  directory = /var/my_nest" >> /home/$USERNAME/.gitconfig

EXPOSE 3000
WORKDIR /var/my_nest
CMD ["npm", "run", "start:dev"]
