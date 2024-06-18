/* SummaryView.css */
.summary-container {
  display: flex;
  justify-content: space-between;
  padding: 20px;
  height: 100vh;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  margin-top: 40px;
  border-radius: 10px;
}

.file-list {
  width: 30%;
  border-right: 10px solid #ccc;
  background-color: rgba(0, 0, 0, 0.5);
  margin-top: 38px;
  padding: 20px;
  border-radius: 10px;
  border-top-right-radius: 0px;
  border-bottom-right-radius: 0px;
  color: white;
}

.file-preview {
  width: 65%;
  padding: 20px;
  margin-top: 38px;
}

.file-item {
  cursor: pointer;
  padding: 10px;
  border-bottom: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.file-item:hover {
  background-color: #f0f0f0;
  color: #000;
}

.file-item span {
  flex-grow: 1;
}

.file-item button {
  margin-left: 10px;
  background-color: red;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  cursor: pointer;
}

.file-item button:hover {
  background-color: darkred;
}

.preview-content {
  text-align: center;
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 10px;
  color: white;
  padding: 20px;
}









import React, { useContext, useState } from 'react';
import { FilesContext } from './FilesContext';
import './SummaryView.css';

export function SummaryView() {
  const { files, setFiles } = useContext(FilesContext);
  const [selectedFile, setSelectedFile] = useState(null);

  const handleFileClick = (file) => {
    setSelectedFile(file);
  };

  const handleFileRemove = (id) => {
    const updatedFiles = files.filter((file) => file.id !== id);
    setFiles(updatedFiles);
    if (selectedFile && selectedFile.id === id) {
      setSelectedFile(null);
    }
  };

  return (
    <div className="summary-container">
      <div className="file-list">
        <h2>Uploaded Documents</h2>
        {files.map((file) => (
          <div key={file.id} className="file-item" onClick={() => handleFileClick(file.file)}>
            <span>{file.file.name}</span>
            <button onClick={(e) => { e.stopPropagation(); handleFileRemove(file.id); }}>Remove</button>
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
                style={{ maxWidth: '100%', maxHeight: '80vh' }}
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
