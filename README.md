.summary-container{
    display: flex;
    justify-content: space-between;
    padding:20px;
    height: 100vh;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  margin-top: 40px;

}

.file-list{
    width:30%;
    border-right: 10px solid #ccc;
    background-color: rgba(0, 0, 0, 0.5);
    margin-top: 38px;
    padding: 20px;
    border-radius: 10px;
    border-top-right-radius: 0px;
    border-bottom-right-radius: 0px;
    
}

.file-preview{
    width: 65%;
    padding: 20px;
}

.file-item{
    cursor: pointer;
    padding: 10px;
    border-bottom: 1px solid #ccc;
}

.file-item:hover{
    background-color: #f0f0f0;
}

.preview-content{
    text-align:center; 
    background-color: rgba(0, 0, 0, 0.5);
    border-radius: 10px;
}










import React, { useContext, useState } from 'react';
import { FilesContext } from './FilesContext';
import './SummaryView.css'; // Create a corresponding CSS file for styling

export function SummaryView() {
  const { files } = useContext(FilesContext);
  const [selectedFile, setSelectedFile] = useState(null);

  const handleFileClick = (file) => {
    setSelectedFile(file);
  };

  return (
    <div className="summary-container">
      <div className="file-list">
        {files.map((file) => (
          <div key={file.id} className="file-item" onClick={() => handleFileClick(file.file)}>
            <span>{file.file.name}</span>
          </div>
        ))}
      </div>
      <div className="file-preview">
        {selectedFile && (
          <div className="preview-content">
            <h2>{selectedFile.name}</h2>
            {selectedFile.type.startsWith("image/") ? (
              <img
                src={URL.createObjectURL(selectedFile)}
                alt={selectedFile.name}
              />
            ) : (
              <iframe
                src={URL.createObjectURL(selectedFile)}
                width="100%"
                height="400px"
                title="file-preview"
              />
            )}
          </div>
        )}
      </div>
    </div>
  );
}
