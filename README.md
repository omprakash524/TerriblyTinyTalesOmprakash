code
import React, { useState } from 'react';
import { Bar } from 'react-chartjs-2';

function App() {
  const [histogramData, setHistogramData] = useState(null);

  const fetchData = async () => {
    try {
      const response = await fetch('https://www.terriblytinytales.com/test.txt');
      const text = await response.text();
      const words = text.toLowerCase().match(/[a-z]+/g); // regex to match words
      const frequencyMap = new Map();

      words.forEach((word) => {
        frequencyMap.set(word, (frequencyMap.get(word) || 0) + 1);
      });

      const sortedWords = Array.from(frequencyMap.entries()).sort((a, b) => b[1] - a[1]).slice(0, 20);

      const labels = sortedWords.map((word) => word[0]);
      const data = sortedWords.map((word) => word[1]);

      setHistogramData({ labels, datasets: [{ data }] });
    } catch (error) {
      console.error(error);
    }
  };

  const downloadCsv = () => {
    const csv = `${histogramData.labels.join(',')}\n${histogramData.datasets[0].data.join(',')}`;
    const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
    const url = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.href = url;
    link.setAttribute('download', 'histogram.csv');
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  };

  return (
    <div>
      <button onClick={fetchData}>Submit</button>
      {histogramData && <Bar data={histogramData} />}
      {histogramData && <button onClick={downloadCsv}>Export</button>}
    </div>
  );
}

export default App;


# TerriblyTinyTalesOmprakash

import React, { useState } from 'react';
import { Bar } from 'react-chartjs-2';
This imports the React library which is used to build the UI, and the Bar component from the react-chartjs-2 library, which is used to create the bar chart.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
function App() {
  const [histogramData, setHistogramData] = useState(null);
This declares a state variable called histogramData, which will store the data for the histogram chart, and a function setHistogramData, which will be used to update the state.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
const fetchData = async () => {
    try {
      const response = await fetch('https://www.terriblytinytales.com/test.txt');
      const text = await response.text();
      const words = text.toLowerCase().match(/[a-z]+/g);
      const frequencyMap = new Map();

      words.forEach((word) => {
        frequencyMap.set(word, (frequencyMap.get(word) || 0) + 1);
      });

      const sortedWords = Array.from(frequencyMap.entries()).sort((a, b) => b[1] - a[1]).slice(0, 20);

      const labels = sortedWords.map((word) => word[0]);
      const data = sortedWords.map((word) => word[1]);

      setHistogramData({ labels, datasets: [{ data }] });
    } catch (error) {
      console.error(error);
    }
  };
This is the function that fetches the text file from the specified URL and parses the data to create the histogram chart. It uses the fetch API to retrieve the text data and the text() method to convert the response to plain text. It then uses a regular expression to match words in the text and create a frequency map using a Map object. It sorts the words in descending order based on frequency using the sort() method, and slices the top 20 words using the slice() method. Finally, it creates the labels and data arrays required by the Bar component and updates the state using the setHistogramData function.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

const downloadCsv = () => {
    const csv = `${histogramData.labels.join(',')}\n${histogramData.datasets[0].data.join(',')}`;
    const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
    const url = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.href = url;
    link.setAttribute('download', 'histogram.csv');
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  };
This function generates a CSV file for exporting the histogram data. It first generates a CSV string using the labels and data arrays from the histogramData state. It then creates a Blob object from the CSV string and generates a URL using the URL.createObjectURL() method. It then creates an a element, sets its href attribute to the generated URL, and sets its download attribute to 'histogram.csv'. It then appends the a element to the DOM, clicks on it to download the file, and removes it from the DOM.


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------


 return (
    <div>
      <button onClick={fetchData}>Submit</button>
      {histogramData && <Bar data={histogramData} />}
      {histogramData && <button onClick={downloadCsv}>Export</button>}
    </div>
  );
}
This is the main component of the app. It renders a
