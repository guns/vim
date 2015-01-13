# -*- encoding: utf-8 -*-
#
# Copyright (c) 2011 Sung Pae <sung@metablu.com>
# Distributed under the MIT license.
# http://www.opensource.org/licenses/mit-license.php

task :default => :configure

desc 'Configure Vim'
task :configure do
  if ENV['DEBUG']
    ENV['CFLAGS'] = '-g -DDEBUG'
  end

  pydir = %x(#{ENV['PYTHON'] || 'python'} -c "import sysconfig; print sysconfig.get_config_var('LIBPL')").chomp

  cmd = %W[
    ./configure
    --prefix=#{ENV['PREFIX'] || '/opt/vim'}
    --enable-rubyinterp=dynamic
    --enable-luainterp=dynamic
    --enable-pythoninterp=dynamic
    --with-python-config-dir=#{pydir}
    --with-features=#{ENV['FEATURES'] || 'huge'}
  ]

  cmd << '--disable-darwin' if RUBY_PLATFORM =~ /darwin/i
  cmd << '--disable-gui' unless ENV['GUI']
  cmd << (ENV['NOX'] ? '--without-x' : '--with-x')

  sh *cmd
end
