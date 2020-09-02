# Docker

How to run various stuff in Docker.

## JRuby

Build and run:

    cd jruby
    docker build -t jruby --build-arg JRUBY_VERSION=9.2.13.0 .
    docker run --rm -it -v "$(pwd):/app" jruby
    docker rmi jruby

Run [Puma] tests (if shared with `-v`) in the container:

    cp -r /app /home && cd /home/app && bundle && bundle e rake compile && JAVA_TOOL_OPTIONS='-Dfile.encoding=UTF8' bundle e rake test:all

Stack Overflow: [Build and run Dockerfile with one command](https://stackoverflow.com/questions/45141402/build-and-run-dockerfile-with-one-command)

[Puma]: https://github.com/puma/puma
