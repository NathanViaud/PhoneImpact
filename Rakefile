require 'squib'
require 'zip'

task default: [:pnp]

desc "Generate Print & Play decks with optional language parameter, the default in French, other options: en"
task :pnp, [:lang] => [:malus, :recap, :events, :recyclage, :pollumoins, :polluplus, :zip]

task :zip, [:lang] do |t, args|
  lang_suffix = args.lang ? ".#{args.lang}" : ""
  zip_filename = "_output/pnp/cards#{lang_suffix}.zip"

  Dir.mkdir('_output/pnp') unless Dir.exist?('_output/pnp')

  pdf_files = [
    "malus#{lang_suffix}.pdf",
    "recap#{lang_suffix}.pdf",
    "events#{lang_suffix}.pdf",
    "recyclage#{lang_suffix}.pdf",
    "pollumoins#{lang_suffix}.pdf",
    "polluplus#{lang_suffix}.pdf"
  ]

  Zip::File.open(zip_filename, Zip::File::CREATE) do |zipfile|
    pdf_files.each do |pdf_file|
      pdf_path = "_output/pnp/#{pdf_file}"
      if File.exist?(pdf_path)
        zipfile.add(pdf_file, pdf_path)
        puts "Added #{pdf_file} to zip"
      else
        puts "Warning: #{pdf_file} not found, skipping"
      end
    end
  end

  puts "Created zip archive: #{zip_filename}"
end

task :malus, [:lang] do |t, args|
    load 'decks/pnp/malus.rb'
    Malus.run(args.lang)
end

task :recap, [:lang] do |t, args|
    load 'decks/pnp/recap.rb'
    Recap.run(args.lang)
end

task :events, [:lang] do |t, args|
    load 'decks/pnp/events.rb'
    Events.run(args.lang)
end

task :recyclage, [:lang] do |t, args|
    load 'decks/pnp/recyclage.rb'
    Recyclage.run(args.lang)
end

task :pollumoins, [:lang] do |t, args|
    load 'decks/pnp/pollumoins.rb'
    Pollumoins.run(args.lang)
end

task :polluplus, [:lang] do |t, args|
    load 'decks/pnp/polluplus.rb'
    Polluplus.run(args.lang)
end

task :zip, [:lang] do |t, args|
    load 'decks/pnp/polluplus.rb'
    Polluplus.run(args.lang)
end

# task :pnp do
#   load 'decks/pnp/malus.rb'
#   load 'decks/pnp/recap.rb'
#   load 'decks/pnp/events.rb'
#   load 'decks/pnp/recyclage.rb'
#   load 'decks/pnp/pollumoins.rb'
#   load 'decks/pnp/polluplus.rb'
# end

task :boiteDeJeu do
  load 'decks/boiteDeJeu/malus.rb'
  load 'decks/boiteDeJeu/recap.rb'
  load 'decks/boiteDeJeu/resources.rb'
  load 'decks/boiteDeJeu/events.rb'
end
