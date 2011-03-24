# Copyright (c) 2011 Sung Pae <sung@metablu.com>
# Distributed under the MIT license.
# http://www.opensource.org/licenses/mit-license.php

verbose false
task :default => :configure

desc 'Configure Vim'
task :configure do
  configure = File.expand_path 'configure'
  abort "Could not execute #{configure.inspect}!" unless File.executable? configure

  # for passing autoconf path variables
  env = {}

  if ENV['RUBY']
    rubylib = %x(#{ENV['RUBY']} -r mkmf -e "print Config::CONFIG['libdir']")
    env['vi_cv_path_ruby'] = ENV['RUBY']
    env['LDFLAGS'] = " -L#{rubylib} "
  end

  env['vi_cv_path_python'] = ENV['PYTHON'] if ENV['PYTHON']

  opts = %W[
    --prefix=#{ENV['PREFIX'] || '/usr/local'}
    --enable-rubyinterp
    --enable-pythoninterp
    --disable-darwin
    --disable-gui
    --with-features=huge
    --with-x
  ]

  # using an alternate X installation?
  opts += %W[
    --x-includes=#{ENV['X11']}/include
    --x-libraries=#{ENV['X11']}/lib
  ] if ENV['X11']

  # show off our command and run it
  puts env.map { |ary| ary.join '=' }.join(' ') + ' \\'
  puts ([configure] + opts).join(" \\\n    ") + "\n\n"
  system env, configure, *opts
end
