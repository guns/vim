# -*- encoding: utf-8 -*-
#
# Copyright (c) 2011 Sung Pae <sung@metablu.com>
# Distributed under the MIT license.
# http://www.opensource.org/licenses/mit-license.php

task :default => :configure

desc 'Configure Vim'
task :configure do
  ENV['CFLAGS' ] ||= ''
  ENV['LDFLAGS'] ||= ''

  if ENV['DEBUG']
    ENV['CFLAGS'] += ' -g -DDEBUG -Wall -Wshadow -Wmissing-prototypes '
  end

  if ENV['RUBY']
    libdir = %x(#{ENV['RUBY']} -r mkmf -e "print RbConfig::CONFIG['libdir']")
    ENV['LDFLAGS'] += " -L#{libdir} "
    ENV['vi_cv_path_ruby'] = ENV['RUBY']
  end

  if ENV['PYTHON']
    ENV['vi_cv_path_python'] = ENV['PYTHON']
  end

  cmd = %W[
    ./configure
    --prefix=#{ENV['PREFIX'] || '/opt/vim'}
    --enable-rubyinterp
    --enable-pythoninterp
    --disable-darwin
    --with-features=#{ENV['FEATURES'] || 'huge'}
    --with-x
  ]

  # Compile without Mac specific features
  if RUBY_PLATFORM =~ /darwin/i
    cmd << '--disable-darwin'
  end

  unless ENV['GUI']
    cmd << '--disable-gui'
  end

  # Specify alternate X installation
  if ENV['X11']
    cmd += %W[--x-includes=#{ENV['X11']}/include --x-libraries=#{ENV['X11']}/lib]
  end

  sh *cmd
end
