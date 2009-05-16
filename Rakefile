require 'rake/clean'

file 'peter-williams.html' => 'peter-williams.md' do 
  `maruku --html peter-williams.md`
end

file 'peter-williams.html_frag' => 'peter-williams.md' do 
  `maruku --html-frag peter-williams.md`
end

file 'peter-williams.pdf' => 'peter-williams.tex' do 
  `pdflatex peter-williams.tex`
end  

file 'peter-williams.tex' => ['peter-williams.md', 'preamble.tex'] do
  `maruku --tex peter-williams.md`
  
  doc = File.read('peter-williams.tex')
  doc.gsub!(/\\begin\{document\}/, "\\begin{document}\n\\scalefont{0.9}\n\\pagestyle{empty}")
  doc.gsub!(/^\s*\n(?=\\end)/m, '')
  doc.gsub!(/(\d{4})\s*\n\s*\n/m, "\\1\n")
  doc.gsub!(/^(Software)/, "\\vspace{0.04in}\n\\1")

  File.open('peter-williams.tex', 'w') do |f|
    f << doc
  end
end

file 'peter-williams.txt' => 'peter-williams.md' do 
  doc = File.read('peter-williams.md') 
  doc.gsub!(/\[([^\]]+)\]\(/, '\1 (')
  doc.gsub!(/\[(.+)\] /, '\1 ') 
  doc.gsub!(/\A.*(Peter)/m, '\1')
  doc.gsub!(/^(peter.williams@barelyenough.org).*$/, '\1')
  doc.gsub!(/^(720.280.2436).*$/, '\1') 
  doc.gsub!(/\*\[[^\n]+\n/, '')
  doc.gsub!(/### (.*)$/) {|s| $1.upcase}

  File.open('peter-williams.txt', 'w') do |f|
    f << doc
  end
end

CLEAN.include('peter-williams.html')
CLEAN.include('peter-williams.html_frag')
CLEAN.include('peter-williams.tex')
CLEAN.include('peter-williams.pdf')
CLEAN.include('peter-williams.txt')
