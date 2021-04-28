BootStrap: docker
From: centos:7

%labels
  Maintainer Manuel Holtgrewe
  R_Version 4.0.5

%apprun R
  exec R "${@}"

%apprun Rscript
  exec Rscript "${@}"

%runscript
  exec R "${@}"

%post
  # Software versions
  export R_VERSION=4.0.5

  # Get dependencies
  yum clean all
  yum upgrade -y
  yum install -y epel-release

  # Configure default locale
  echo 'LANG="en_US.UTF-8"' >/etc/locale.conf
  export LC_ALL=en_US.UTF-8
  export LANG=en_US.UTF-8

  # Install R
  curl -O https://cdn.rstudio.com/r/centos-7/pkgs/R-${R_VERSION}-1-1.x86_64.rpm
  yum install -y R-${R_VERSION}-1-1.x86_64.rpm
  rm -f R-${R_VERSION}-1-1.x86_64.rpm
  ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R
  ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript

  # Add a default CRAN mirror
  echo "options(repos = c(CRAN = 'https://cran.rstudio.com/'), download.file.method = 'libcurl')" >> /opt/R/${R_VERSION}/lib/R/etc/Rprofile.site

  # Add a directory for host R libraries
  mkdir -p /library
  echo "R_LIBS_SITE=/library:\${R_LIBS_SITE}" >> /opt/R/${R_VERSION}/lib/R/etc/Renviron.site

  # Clean up
  yum clean all
