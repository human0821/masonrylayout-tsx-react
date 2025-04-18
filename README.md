## Masonry layout for images and videos. Live demo: https://ivanpk938.vercel.app/masonry

## Example
```js

import MasonryLayout, {MasonryLayoutRefType} from "./masonrylayout-tsx-react";
import {FC, useRef, useState} from "react";

const key = () => String(Math.random()).split('.')[1];
const box = {width: '300px'};
const button = {padding: '10px', cursor: 'pointer', border: '1px solid transparent', margin: '20px 5px'};
const assetStyle = {width: '100%', display: 'flex', borderRadius: '7px'};
const centrify = {display: 'flex', justifyContent: 'center', alignItems: 'center'};

const externalLinks = [
  'https://i.imgur.com/m884zzP.mp4',
  'https://images.unsplash.com/photo-1682687220866-c856f566f1bd?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1699378999301-8c88a6a237d9?q=80&w=1364&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://plus.unsplash.com/premium_photo-1680553491336-644d5955ea50?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1683009427666-340595e57e43?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://plus.unsplash.com/premium_photo-1673435845965-66513400985f?q=80&w=1332&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1699275303964-a9a1a8ae8c6b?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1699111260849-f7e9cdfc1bde?q=80&w=1374&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1699030665523-e9c8a366b9a3?q=80&w=1332&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1699355746758-9f9572a3e40e?q=80&w=1374&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1682688759157-57988e10ffa8?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1699192693656-d7fb172ff07f?q=80&w=1374&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1699111259969-5b4c94447c38?q=80&w=1374&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1699111156364-021c7878a2cd?q=80&w=1374&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1699116550661-bea051952f96?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1682686581264-c47e25e61d95?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxlZGl0b3JpYWwtZmVlZHwxfHx8ZW58MHx8fHx8',
  'https://plus.unsplash.com/premium_photo-1699292639215-6f34ff51daec?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1682685796444-acc2f5c1b7b6?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  'https://plus.unsplash.com/premium_photo-1683309568218-bf32f6d904f0?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwyNHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=700&q=60',
  'https://images.unsplash.com/photo-1699462515808-41f81a8145b0?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
];

const Page: FC = () => {
  const [links, setLinks] = useState<string[]>(externalLinks);
  const ref = useRef<MasonryLayoutRefType>(null);
  const updateLayout = () => ref.current?.layout();

  const addLink = () => setLinks(links => [externalLinks[1], ...links]);
  const removeLink = () => setLinks(links => links.slice(1));

  return <div>
    <div style={centrify}>
      <button style={button} onClick={addLink}>Add</button>
      <button style={button} onClick={removeLink}>Remove</button>
    </div>
    <MasonryLayout forwardedRef={ref} animate=".4s ease" justifyContainer="center" gap={5} layoutThrottle={200}>
      {links.map((link, i) => <div key={i} style={box}>
        {/\.mp4$/.test(link)
          ? <video onLoadedMetadata={updateLayout} controls={true} autoPlay={true} loop={true} muted style={assetStyle}><source src={link} type="video/mp4" /></video>
          : <img onLoad={updateLayout} style={assetStyle} src={link} />
        }</div>
      )}
    </MasonryLayout>
  </div>
}

export default Page;
```

## Props

| property | type | default | description |
| --- | --- | --- | --- |
| `forwardedRef` | RefObject\<MasonryLayoutRefType\> | none | Provides **layout()** function. Used to layout elements |
| `animate` | string | none | To animate elements using CSS-transition. Example: **.4s ease** |
| `justifyContainer` | 'flex-start' \| 'center' \| 'flex-end' | 'flex-start' | Specifies how to place container (in which all elements are nested) |
| `gap` | number | 10 | A gap for the elements |
| `layoutThrottle` | number | 250 | Delay after which the **layout()** function is called to layout elements when browser's window is resized | 

## TODO:
Enable animations only when all images/videos loaded
