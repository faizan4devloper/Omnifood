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
    {breadcrumbs.map(({ match, breadcrumb }, index) => (
      <span key={match.pathname}>
        <Link to={match.pathname}>{breadcrumb}</Link>
        {index < breadcrumbs.length - 1 && ' / '}
      </span>
    ))}
  </nav>
);

export { routes, Breadcrumbs };





import React, { useState } from "react";
import "./App.css";
import { BrowserRouter, Routes, Route, useLocation } from "react-router-dom";
import { Header } from "./components/Landing/Header";
import { Hero } from "./components/Landing/Hero"; 
import { NewClaimPage } from "./NewClaimPage";
import { SummaryView } from "./SummaryView";
import { FilesProvider } from "./FilesContext";
import { Footer } from "./components/Landing/Footer";
import getBreadcrumbs from "react-router-breadcrumbs-hoc";
import { routes, Breadcrumbs } from "./breadcrumbs";

function App() {
  const [selectedDocument, setSelectedDocument] = useState(null);

  const handleDocumentSelect = (document) => {
    setSelectedDocument(document);
  };

  const location = useLocation();
  const breadcrumbs = getBreadcrumbs(routes, location.pathname);

  return (
    <div>
      <Header />
      <FilesProvider>
        <Breadcrumbs breadcrumbs={breadcrumbs} />
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
    </div>
  );
}

export default App;
