require 'guard/plugin'

module ::Guard
  class LessWatcher < ::Guard::Plugin

    def start
      run_on_changes([])
    end

    def reload
      start
    end

    def run_on_changes(paths)
      dest_path = "source/stylesheets/all.less"
      return if paths == [dest_path]

      next_number = if File.exists?(dest_path)
        contents = File.read(dest_path)
        if contents =~ %r{// (\d+)}
          $1.to_i + 1
        end
      end

      next_number = next_number.to_i

      template = File.read("source/stylesheets/all-template.less")

      File.open(dest_path, 'w') do |file|
        file.write(template.gsub(%r{// (\d+)}) { "// #{next_number}"})
      end
    end
  end
end

guard :less_watcher do
  watch(%r{^source/stylesheets/(.+)\.less$})
end
