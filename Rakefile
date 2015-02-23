require 'html/proofer'

task default: %w[test]

task :build do
	sh "bundle exec jekyll build"
end

task :test => :build do
	options = {
		:href_ignore => [/.*localhost.*/, /.*www.psimer.net.*/]
	}
	HTML::Proofer.new("./_site", options).run
end
