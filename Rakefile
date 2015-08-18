require 'html/proofer'

task default: %w[test]

task :build do
	sh "bundle exec jekyll build"
end

task :serve do
	sh "bundle exec jekyll serve -D"
end

task :test => :build do
	options = {
		:href_ignore => [/.*localhost.*/, /.*www.psimer.net.*/, /.*www.linkedin.com.*/]
	}
	HTML::Proofer.new("./_site", options).run
end
