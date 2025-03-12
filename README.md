import { useState } from "react";
import Image from "next/image";
import { Card } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Play, Pause, Scissors, Upload, Sliders, Volume2, Settings } from "lucide-react";

export default function VideoEditor() {
  const [isPlaying, setIsPlaying] = useState(false);
  const [hue, setHue] = useState(0);
  const [saturation, setSaturation] = useState(100);
  const [bitrate, setBitrate] = useState(5000);
  const [fps, setFps] = useState(30);
  const supportedFormats = [
    "MP4", "MOV", "AVI", "MPEG", "WMV", "264", "3GP", "3GPP", "AVC", "AVI", 
    "F4V", "FLV", "M4V", "MOV", "MP4", "MPE", "MPEG", "MPG", "MTS", "MXF", 
    "R3D", "TS", "VOB", "WM", "WMV"
  ];

  return (
    <div className="flex flex-col h-screen bg-gray-900 text-white">
      {/* Top Toolbar */}
      <div className="p-2 bg-gray-800 flex items-center justify-between">
        <div className="flex items-center">
          <Image 
            src="/mnt/data/Screenshot_2025-03-12_at_11.13.59_PM-removebg-preview.png" 
            alt="DG Editor Logo" 
            width={50} 
            height={50} 
            className="mr-2"
          />
          <h2 className="text-lg font-bold">Video Editor</h2>
        </div>
        <Button variant="outline" className="flex items-center">
          <Upload className="w-4 h-4 mr-2" /> Import Media
        </Button>
      </div>
      
      {/* Main Editor Layout */}
      <div className="flex flex-1">
        {/* Media Library */}
        <Card className="w-1/4 p-4 bg-gray-700">
          <h3 className="text-lg font-bold mb-2">Media Library</h3>
          <p className="text-sm">Supported Formats:</p>
          <ul className="text-xs list-disc pl-4">
            {supportedFormats.map((format) => (
              <li key={format}>{format}</li>
            ))}
          </ul>
        </Card>
        
        {/* Preview & Timeline Area */}
        <div className="flex flex-col flex-1 p-4">
          {/* Preview Window */}
          <Card className="flex items-center justify-center h-64 bg-black">
            <span>Video Preview</span>
          </Card>
          
          {/* Timeline */}
          <Card className="flex items-center justify-between p-4 mt-4 bg-gray-800">
            <Button onClick={() => setIsPlaying(!isPlaying)}>
              {isPlaying ? <Pause /> : <Play />}
            </Button>
            <Button variant="outline">
              <Scissors className="w-4 h-4" /> Cut
            </Button>
          </Card>
        </div>
        
        {/* Color Correction Panel */}
        <Card className="w-1/4 p-4 bg-gray-700 flex flex-col items-start">
          <h3 className="text-lg font-bold mb-2">Color Correction</h3>
          <Button variant="outline" className="flex items-center w-full mb-4">
            <Sliders className="w-4 h-4 mr-2" /> Adjust Colors
          </Button>
          <label className="w-full text-sm">Hue</label>
          <input
            type="range"
            min="-180"
            max="180"
            value={hue}
            onChange={(e) => setHue(e.target.value)}
            className="w-full mb-2"
          />
          <label className="w-full text-sm">Saturation</label>
          <input
            type="range"
            min="0"
            max="200"
            value={saturation}
            onChange={(e) => setSaturation(e.target.value)}
            className="w-full"
          />
        </Card>

        {/* Audio Enhancement Panel */}
        <Card className="w-1/4 p-4 bg-gray-700 flex flex-col items-start">
          <h3 className="text-lg font-bold mb-2">Audio Enhancement</h3>
          <Button 
            variant="outline" 
            className="flex items-center w-full mb-4"
            onClick={() => window.open('https://podcast.adobe.com/enhance#', '_blank')}
          >
            <Volume2 className="w-4 h-4 mr-2" /> Enhance Audio
          </Button>
        </Card>
      </div>

      {/* Video Export Panel */}
      <Card className="p-4 bg-gray-800 flex flex-col items-start mt-4">
        <h3 className="text-lg font-bold mb-2">Export Settings</h3>
        <label className="w-full text-sm">Choose Bitrate (kbps)</label>
        <input
          type="number"
          min="1000"
          max="50000"
          value={bitrate}
          onChange={(e) => setBitrate(e.target.value)}
          className="w-full mb-2 p-1 text-black"
        />
        <label className="w-full text-sm">Choose FPS</label>
        <input
          type="number"
          min="24"
          max="120"
          value={fps}
          onChange={(e) => setFps(e.target.value)}
          className="w-full mb-2 p-1 text-black"
        />
        <Button variant="outline" className="mt-2 flex items-center">
          <Settings className="w-4 h-4 mr-2" /> Export Video
        </Button>
      </Card>
    </div>
  );
}
