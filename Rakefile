# coding: utf-8

require 'digest/sha1'

SPACE_STRING = " "
TRUE_STRING = "TRUE"
FALSE_STRING = "FALSE"
CSC_STRING = " : "

desc "*.flv なファイルを sha1 チェックして重複の管理を行う"
task :sha1_create do
  open("sha1.txt", "w") { |log|
    Dir.glob("*.flv").each do |file|
      filename = File.basename(file)
      log.puts filename + SPACE_STRING + Digest::SHA1.hexdigest(File.binread(filename));
    end
  }
end

desc "作成した sha1 リストから重複を探す"
task :sha1_check do

  hash = Hash.new()
  array = Array.new

  open("sha1.txt", "r:utf-8") { |log|
    while line = log.gets
      print line
      s = line.split(' ')
      if s.length == 2 then
        if hash[s[1]] != nil then
          array[array.length] = s
          # print TRUE_STRING + CSC_STRING + line
        else
          hash[s[1]] = s[0]
          # print FALSE_STRING + CSC_STRING + line
        end
      end
    end
  }
  open("delete.txt", "w") { |result|
    for line in array do
      for v in line do
        result.print v
        result.print " "
      end
      result.puts ""
    end
  }
end
