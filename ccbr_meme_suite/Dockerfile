FROM ubuntu:18.04

# Here is an exhaustive list of everything MEME Suite needs: http://meme-suite.org/doc/install.html?man_type=web#prerequisite

RUN mkdir -p /data
RUN mkdir -p /opt

# Using apt-get to install a few packages
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    libopenmpi-dev \
    openmpi-bin \
    ghostscript \
    libgs-dev \
    libgd-dev \
    libexpat1-dev \
    zlib1g-dev \
    libxml2-dev \
    autoconf automake libtool \
    libhtml-template-compiled-perl \
    libxml-opml-simplegen-perl \
    libxml-libxml-debugging-perl \
    sudo \
    openssh-server

RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install Log::Log4perl'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install Math::CDF'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install CGI'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install HTML::PullParser'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install HTML::Template'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install XML::Simple'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install XML::Parser::Expat'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install XML::LibXML'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install XML::LibXML::Simple'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install XML::Compile'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install XML::Compile::SOAP11'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install XML::Compile::WSDL11'
RUN PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install XML::Compile::Transport::SOAPHTTP'
RUN mkdir /opt/meme

# Get MEME Suite TAR file
ADD http://meme-suite.org/meme-software/5.0.4/meme-5.0.4.tar.gz /opt/meme

WORKDIR /opt/meme/

# Unpack Tar
RUN tar zxvf meme-5.0.4.tar.gz && rm -fv meme-5.0.4.tar.gz

# Configure, build and install MEME Suite 
RUN cd /opt/meme/meme-5.0.4 && \
	./configure --prefix=/opt  --enable-build-libxml2 --enable-build-libxslt  --with-url=http://meme-suite.org && \ 
	make && \
	make install && \
        rm -rfv /opt/meme

# Adding MEME SUITE to $PATH 
ENV PATH="/opt/bin:${PATH}"

# Setting language environment variable
ENV LANG en_US.UTF-8 

WORKDIR /opt
COPY Dockerfile /opt

WORKDIR /data
