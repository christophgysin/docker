# VERSION:        1.6
# DOCKER-VERSION  0.6.6
# AUTHOR:         Daniel Mizyrycki <daniel@docker.com>
# DESCRIPTION:    Build docker nightly release using Docker in Docker.
# REFERENCES:     This code reuses the excellent implementation of docker in docker
#                 made by Jerome Petazzoni.  https://github.com/jpetazzo/dind
# COMMENTS:
#   release_credentials.json is a base64 json encoded file containing:
#       { "AWS_ACCESS_KEY": "Test_docker_AWS_S3_bucket_id",
#         "AWS_SECRET_KEY": "Test_docker_AWS_S3_bucket_key",
#         "GPG_PASSPHRASE": "Test_docker_GPG_passphrase_signature" }
# TO_BUILD:       docker build -t dockerbuilder .
# TO_RELEASE:     docker run -i -t -privileged -e AWS_S3_BUCKET="test.docker.io" dockerbuilder hack/dind dockerbuild.sh

from docker
maintainer Daniel Mizyrycki <daniel@docker.com>

# Add docker dependencies and downloading packages
run echo 'deb http://archive.ubuntu.com/ubuntu precise main universe' > /etc/apt/sources.list
run apt-get update; apt-get install -y -q wget python2.7

# Add production docker binary
run wget -q -O /usr/bin/docker http://get.docker.io/builds/Linux/x86_64/docker-latest; chmod +x /usr/bin/docker

# Add proto docker builder
add ./dockerbuild.sh /usr/bin/dockerbuild.sh
run chmod +x /usr/bin/dockerbuild.sh

# Add release credentials
add ./release_credentials.json /root/release_credentials.json
