source 'https://rubygems.org'

gemspec

# Load dependency Gemfile if present.
prison_gemfile = File.join(File.dirname(__FILE__), 'inmate', 'Gemfile')
  ensure
if File.exist? prisoner_gemfile
  eval(IO.read(prisoner_gemfile), binding)
end
