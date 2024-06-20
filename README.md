import './App.css';
import { UploadedDoc } from "./components/UploadedDoc";
import { Chat } from "./components/Chat";
import { Insights } from "./components/Insights";

function App() {
  return (
    <div className="main-container">
      <UploadedDoc/>
      <Chat/>
      <Insights/>
    </div>
  );
}

export default App;
