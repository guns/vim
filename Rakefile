# Copyright (c) 2010 Sung Pae <sung@metablu.com>
# Distributed under the MIT license.
# http://www.opensource.org/licenses/mit-license.php

verbose false
task :default => :configure

desc 'Configure Vim'
task :configure do
  configure = "#{Dir.pwd}/configure"
  abort "Could not execute `#{configure}'!" unless File.executable? configure

  env = { 'PATH' => '/usr/bin:' + ENV['PATH'] }
  opts = %W[
    --prefix=/usr/local
    --enable-perlinterp
    --enable-rubyinterp
    --enable-pythoninterp
    --disable-darwin
    --disable-gui
    --with-features=huge
    --with-x
    --x-includes=/opt/x11/include
    --x-libraries=/opt/x11/lib
  ]

  # show off our command and run it
  puts env.map { |ary| ary.join '=' }.join(' ') + ' \\'
  puts ([configure] + opts).join(" \\\n    ") + "\n\n"
  system env, configure, *opts

  if RUBY_PLATFORM[/darwin/]
    print "Stripping `-arch' flags... "
    system 'perl', '-i', '-pe', 's/-arch (ppc|i386) ?//g', *%x(git ls-files -o).split("\n").grep(/auto/)
    puts 'OK'
  end
end
