require "rubygems"
require "bundler/setup"

Bundler.require(:default)

require "ostruct"
require "fileutils"

ERRORS = {
  400 => {
    title: "Bad Request",
    subtitle: "There was an error in the request"
  },
  401 => {
    title: "Authorization Required",
    subtitle: "The request did not include the required authentication headers"
  },
  403 => {
    title: "Forbidden",
    subtitle: "You are not authorised to see this content"
  },
  404 => {
    title: "Not found",
    subtitle: "We can't find the thing you're looking for…"
  },
  410 => {
    title: "Gone",
    subtitle: "Something used to be here, but it's gone now"
  },
  500 => {
    title: "Internal Server Error",
    subtitle: "Uh oh. Something exploded on our end."
  },
  501 => {
    title: "Not Implemented",
    subtitle: "Whoops, we haven't got around to making this work"
  },
  502 => {
    title: "Bad Gateway",
    subtitle: "The server you're trying to reach is sending back errors"
  },
  503 => {
    title: "Service Unavailable",
    subtitle: "The service is currently unreachable. Check back later."
  },
  504 => {
    title: "Gateway Timeout",
    subtitle: "The gateway has timed out"
  },
  505 => {
    title: "HTTP Version Not Supported",
    subtitle: "The HTTP protocol you are asking for is not supported"
  },
  "maintenance" => {
    title: "Application Offline for Maintenance",
    subtitle: "This application is undergoing maintenance right now.  Please check back later."
  },
}

desc "Build the error and maintenance pages"
task :build do
  FileUtils.mkdir_p("./build")

  ERRORS.each do |code, props|
    scope = OpenStruct.new
    scope.code = code
    scope.properties = props

    filename = "./build/#{code}.html"

    File.open("./build/#{code}.html", "wb") do |f|
      f.write Slim::Template.new("template.slim", pretty: false).render(scope)
      f.write "\n"
    end

    puts "Generated #{filename}"
  end
end

task default: :build
