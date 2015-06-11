require 'fileutils'

namespace :post do
	desc "Starting a new post draft."
	task :new do
		puts "What's the post title?"
		@name = STDIN.gets.chomp
		@slug = "#{@name}"
		@slug = @slug.tr('ÁáÉéÍíÓóÚú', 'AaEeIiOoUu')
		@slug = @slug.downcase.strip.gsub(' ', '-')
		FileUtils.touch("_drafts/#{@slug}.md")

		open("_drafts/#{@slug}.md", 'w' ) do |file|
			file.puts "---"
			file.puts "layout: post"
			file.puts "title: #{@name}"
			file.puts "category: blog"
			file.puts "tag: blog"
			file.puts "---"
		end

		system ("#{ENV['EDITOR']} _drafts/#{@slug}.md")
	end

	desc "Publish an existing draft."
	task :publish do
		puts "Post(s) in _drafts:"
		Dir.foreach("_drafts") do |fname|
			next if fname == '.' or fname == '..' or fname == '.keep'
			puts fname
		end

		puts "Post which draft?"
		@post_name = STDIN.gets.chomp
		@post_date = Time.now.strftime("%F")
		FileUtils.mv("_drafts/#{@post_name}", "_posts/#{@post_date}-#{@post_name}")
		puts "Done!"
	end
end

task :default do
	puts "Don't do that."
end
