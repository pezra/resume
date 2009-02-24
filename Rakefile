file 'peter-williams.pdf' => 'peter-williams.tex' do 
  `pdflatex peter-williams.tex`
end  

file 'peter-williams.tex' => 'peter-williams.md' do
  `maruku --tex peter-williams.md`
  
  doc = File.read('peter-williams.tex')
  doc.gsub!(/\\begin\{document\}/, "\\begin{document}\n\\scalefont{0.75}\n\\pagestyle{empty}")
  doc.gsub!(/^\s*\n(?=\\end)/m, '')
  doc.gsub!(/(\d{4})\s*\n\s*\n/m, "\\1\n")
  doc.gsub!(/^(Software)/, "\\vspace{0.04in}\n\\1")x

  File.open('peter-williams.tex', 'w') do |f|
    f << doc
  end
end


task :clean do 
  rm 'peter-williams.tex'
  rm 'peter-williams.pdf'
end
