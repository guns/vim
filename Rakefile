# Copyright (c) 2010 Sung Pae <sung@metablu.com>
# Distributed under the MIT license.
# http://www.opensource.org/licenses/mit-license.php

verbose false
task :default => :configure

desc 'Configure Vim'
task :configure do
  configure = File.expand_path 'configure'
  abort "Could not execute #{configure.inspect}!" unless File.executable? configure

  env = { 'PATH' => '/usr/bin:' + ENV['PATH'] }

  opts = %w[
    --prefix=/usr/local
    --enable-rubyinterp
    --enable-pythoninterp
    --disable-darwin
    --disable-gui
    --with-features=huge
    --with-x
  ]

  opts += %w[
    --x-includes=/opt/X11/include
    --x-libraries=/opt/X11/lib
  ] if File.directory? '/opt/X11'

  # show off our command and run it
  puts env.map { |ary| ary.join '=' }.join(' ') + ' \\'
  puts ([configure] + opts).join(" \\\n    ") + "\n\n"
  system env, configure, *opts
end
