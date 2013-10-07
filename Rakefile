require "rake/testtask"
require "appraisal"

REDIS_DIR = File.expand_path(File.join("..", "test"), __FILE__)
REDIS_CNF = File.join(REDIS_DIR, "test.conf")
REDIS_PID = File.join(REDIS_DIR, "db", "redis.pid")

task :default => :run

desc "Run tests and manage server start/stop"
task :run => [:start, :test, :stop]

desc "Start the Redis server"
task :start do
  unless File.exists?(REDIS_PID)
    system "redis-server #{REDIS_CNF}"
  end
end

desc "Stop the Redis server"
task :stop do
  if File.exists?(REDIS_PID)
    system "kill #{File.read(REDIS_PID)}"
    File.delete(REDIS_PID)
  end
end

Rake::TestTask.new do |t|
  t.libs << "test"
  t.test_files = FileList['test/*_test.rb']
  t.verbose = true
end
