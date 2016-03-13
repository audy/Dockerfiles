FROM centos

# following http://www.pacb.com/wp-content/uploads/2015/09/SMRT-Analysis-Software-Installation-v2.3.0.pdf

MAINTAINER harekrishna@gmail.com

ENV SMRT_ROOT=/opt/smrtanalysis/
ENV SMRT_USER=smrtanalysis
ENV SMRT_GROUP=smrtanalysis

RUN yum groupinstall -y "Development Tools"
RUN yum install -y redhat-lsb net-tools

RUN groupadd $SMRT_GROUP
RUN adduser \
  --gid $SMRT_GROUP \
  --home-dir $SMRT_ROOT \
  --create-home \
  --shell /bin/bash \
  $SMRT_USER

USER $SMRT_USER
WORKDIR $SMRT_ROOT

RUN curl -LO -# \
  http://files.pacb.com/software/smrtanalysis/2.3.0/smrtanalysis_2.3.0.140936.run

RUN curl -LO -# \
  https://s3.amazonaws.com/files.pacb.com/software/smrtanalysis/2.3.0/smrtanalysis-patch_2.3.0.140936.p5.run

RUN bash \
  smrtanalysis_2.3.0.140936.run \
  -p smrtanalysis-patch_2.3.0.140936.p5.run \
  --rootdir $SMRT_ROOT \
  --batch \
  --ignore-syscheck \
  --jmstype NONE

ADD ./run .

EXPOSE 8080

ENTRYPOINT ["./run"]
