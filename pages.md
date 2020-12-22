---
layout: page
---
<html>
  <body>
    <div>
      <h2>MarkDown Pages</h2>
      <ul id="md_list">
      </ul>
    </div>
    
    <div>
      <h2>HTML Pages</h2>
      <ul id="html_list">
      </ul>
    </div>
    
    <script>
      const filterFiles = (filter_md) => {
        filter = filter.toLowerCase()
        return (file) => {
          const filePath = file.path;
          const fileName = file.path.replace('.md', '').toLowerCase().replace(/-/g, ' ');
          const isMD = (/.md$/).test(filePath);
          const isNotREADME = filePath !== 'README.md';
          return isMD && isNotREADME;
        }
      }
      
      const renderList = (data, filter = '') => {
        let htmlString = '<ul>';
        for (let file of data.filter(filterFiles(filter_md))) {
          const filePath = file.path;
          const fileName = file.path.replace('.md', '').toLowerCase().replace(/-/g, ' ');
          htmlString += `<li><a href="${filePath}">${fileName}</a></li>`;
        }
      htmlString += '</ul>';
        document.getElementById('md_list').innerHTML = htmlString;
      }
      
      const filterFiles = (filter_html) => {
        filter = filter.toLowerCase()
        return (file) => {
          const filePath = file.path;
          const fileName = file.path.replace('.html', '').toLowerCase().replace(/-/g, ' ');
          const isHTML = (/.html$/).test(filePath);
          return isHTML;
        }
      }
      
      const renderList = (data, filter = '') => {
        let htmlString = '<ul>';
        for (let file of data.filter(filterFiles(filter_html))) {
          const filePath = file.path;
          const fileName = file.path.replace('.html', '').toLowerCase().replace(/-/g, ' ');
          htmlString += `<li><a href="${filePath}">${fileName}</a></li>`;
        }
      htmlString += '</ul>';
        document.getElementById('html_list').innerHTML = htmlString;
      }
      
      (async () => {
        const response = await fetch('https://api.github.com/repos/b-kennedy0/b-kennedy0.github.io/contents/');
        const data = await response.json();
        renderList(data);
      })()
    </script>
  <body>
</html>
