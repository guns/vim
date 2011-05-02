# Copyright (c) 2011 Sung Pae <sung@metablu.com>
# Distributed under the MIT license.
# http://www.opensource.org/licenses/mit-license.php

def execute env, cmd
  puts (env.map { |k,v| "#{k}=#{v.inspect}" } + cmd).join(' ')

  if RUBY_VERSION < '1.9'
    env.each { |k,v| ENV[k] = v }
    system *cmd
  else
    system env, *cmd
  end
end

verbose false
task :default => :configure

desc 'Configure Vim'
task :configure do
  # for passing autoconf path variables
  env = {}

  if ENV['DEBUG']
    env['CFLAGS'] = '-g -DDEBUG -Wall -Wshadow -Wmissing-prototypes'
  end

  if ENV['RUBY']
    rubylib = %x(#{ENV['RUBY']} -r mkmf -e "print Config::CONFIG['libdir']")
    env['vi_cv_path_ruby'] = ENV['RUBY']
    env['LDFLAGS'] = " -L#{rubylib} "
  end

  if ENV['PYTHON']
    env['vi_cv_path_python'] = ENV['PYTHON']
  end

  cmd = %W[
    #{File.expand_path 'configure'}
    --prefix=#{ENV['PREFIX'] || '/opt/vim'}
    --enable-rubyinterp
    --enable-pythoninterp
    --disable-darwin
    #{'--disable-gui' unless ENV['GUI']}
    --with-features=#{ENV['FEATURES'] || 'huge'}
    --with-x
  ]

  # using an alternate X installation?
  cmd += %W[
    --x-includes=#{ENV['X11']}/include
    --x-libraries=#{ENV['X11']}/lib
  ] if ENV['X11']

  execute env, cmd
end
