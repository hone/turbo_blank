require 'bundler/setup'
require 'helix_runtime/build_task'
require 'rake/testtask'

HelixRuntime::BuildTask.new("turbo_blank") 

task :benchmark => :build do
  exec "ruby -Ilib benchmark.rb"
end

Rake::TestTask.new(:test) do |t|
  t.libs << "test"
  t.libs << "lib"
  t.test_files = FileList["test/**/*_test.rb"]
end

task :test => :build

task "test:all" do
  ['RUST', 'RAILS_4_2', 'RAILS_5'].each do |impl|
    sh({ 'IMPLEMENTATION' => impl }, 'rake test')
  end
end

task :default => "test:all"

task :default => :build
