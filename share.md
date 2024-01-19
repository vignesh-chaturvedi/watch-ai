import React, { useState, useEffect } from 'react';

const getRandomColor = () => {
  const letters = '0123456789ABCDEF';
  let color = '#';
  for (let i = 0; i < 6; i++) {
    color += letters[Math.floor(Math.random() * 16)];
  }
  return color;
};

const App = () => {
  const [backgroundColor, setBackgroundColor] = useState(localStorage.getItem('backgroundColor') || '#ffffff');
  const [intervalId, setIntervalId] = useState(null);

  const startChangingColor = () => {
    const id = setInterval(() => {
      setBackgroundColor(getRandomColor());
    }, 1000);
    setIntervalId(id);
  };

  const stopChangingColor = () => {
    clearInterval(intervalId);
    localStorage.setItem('backgroundColor', backgroundColor);
  };

  useEffect(() => {
    return () => {
      clearInterval(intervalId);
    };
  }, [intervalId]);

  return (
    <div style={{ backgroundColor, height: '100vh' }}>
      <button onClick={startChangingColor}>Start</button>
      <button onClick={stopChangingColor}>Stop</button>
    </div>
  );
};

export default App;