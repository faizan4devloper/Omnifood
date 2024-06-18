import React from 'react';
import './Pagination.css'; // Import the styles for pagination

const Pagination = ({ currentPage, totalPages, onPageChange }) => {
  const pages = [];
  for (let i = 1; i <= totalPages; i++) {
    pages.push(i);
  }

  return (
    <div className="pagination">
      {pages.map((page) => (
        <button
          key={page}
          className={page === currentPage ? 'active' : ''}
          onClick={() => onPageChange(page)}
        >
          {page}
        </button>
      ))}
    </div>
  );
};

export default Pagination;


.pagination {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.pagination button {
  margin: 0 5px;
  padding: 10px 15px;
  border: none;
  background-color: #6f36cd;
  color: white;
  cursor: pointer;
  border-radius: 5px;
}

.pagination button.active {
  background-color: #1f77f6;
}

.pagination button:hover {
  background-color: #45260a;
}





import React, { useState } from 'react';
import './App.css'; // Import global styles
import Pagination from './Pagination'; // Import Pagination component
import { NewClaimPage } from './NewClaimPage'; // Import NewClaimPage component
import { SummaryView } from './SummaryView'; // Import SummaryView component

const App = () => {
  const [currentPage, setCurrentPage] = useState(1);
  const totalPages = 3; // Total number of pages

  const renderPage = () => {
    switch (currentPage) {
      case 1:
        return <NewClaimPage />;
      case 2:
        return <SummaryView />;
      case 3:
        return <div>Page 3 Content</div>; // Replace with your third page component
      default:
        return <NewClaimPage />;
    }
  };

  return (
    <div className="app">
      {renderPage()}
      <Pagination
        currentPage={currentPage}
        totalPages={totalPages}
        onPageChange={setCurrentPage}
      />
    </div>
  );
};

export default App;





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































//
import React, { useState } from "react";
import "./App.css"
import { BrowserRouter, Routes, Route } from "react-router-dom";

import { Header } from "./components/Landing/Header";
import { Hero } from "./components/Landing/Hero"; 
import { NewClaimPage } from "./NewClaimPage";
import { SummaryView } from "./SummaryView";
import { FilesProvider } from "./FilesContext";
import { Footer } from "./components/Landing/Footer";


function App() {
  const [selectedDocument, setSelectedDocument] = useState(null);

  const handleDocumentSelect = (document) => {
    setSelectedDocument(document);
  };

  return (
    <BrowserRouter>
      <Header />
      <FilesProvider>
        
      <Routes>
        <Route path="/" element={
          <Hero onDocumentSelect={handleDocumentSelect} />
        } />
        
        <Route path="/NewClaimPage" element={
          <NewClaimPage />  
        } />
        <Route path="summary" element={<SummaryView/>} />
      </Routes>
      </FilesProvider>
      
      <Footer />
    </BrowserRouter>
  );
}

export default App;























// src/breadcrumbs.js
import React from 'react';
import { Link } from 'react-router-dom';

const routes = [
  { path: '/', breadcrumb: 'Home' },
  { path: '/NewClaimPage', breadcrumb: 'New Claim' },
  { path: '/summary', breadcrumb: 'Summary' },
];

const Breadcrumbs = ({ breadcrumbs }) => (
  <nav>
    {breadcrumbs.map(({ match, breadcrumb }) => (
      <span key={match.pathname}>
        <Link to={match.pathname}>{breadcrumb}</Link>
        {' / '}
      </span>
    ))}
  </nav>
);

export { routes, Breadcrumbs };



import React, { useState } from "react";
import "./App.css";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { Header } from "./components/Landing/Header";
import { Hero } from "./components/Landing/Hero"; 
import { NewClaimPage } from "./NewClaimPage";
import { SummaryView } from "./SummaryView";
import { FilesProvider } from "./FilesContext";
import { Footer } from "./components/Landing/Footer";
import { withBreadcrumbs } from "react-router-breadcrumbs-hoc";
import { routes, Breadcrumbs } from "./breadcrumbs";

function App() {
  const [selectedDocument, setSelectedDocument] = useState(null);

  const handleDocumentSelect = (document) => {
    setSelectedDocument(document);
  };

  const BreadcrumbsComponent = withBreadcrumbs(routes)(Breadcrumbs);

  return (
    <BrowserRouter>
      <Header />
      <FilesProvider>
        <BreadcrumbsComponent />
        <Routes>
          <Route path="/" element={
            <Hero onDocumentSelect={handleDocumentSelect} />
          } />
          <Route path="/NewClaimPage" element={
            <NewClaimPage />  
          } />
          <Route path="/summary" element={<SummaryView />} />
        </Routes>
      </FilesProvider>
      <Footer />
    </BrowserRouter>
  );
}

export default App;
