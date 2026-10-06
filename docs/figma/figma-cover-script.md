# Figma cover — ready-to-run script

File: Abadin — Design System (`Qwx3QpLbhwbouq12QLvAL5`), Cover page `0:1`.

**Status:** not yet run. The Starter-plan MCP call limit blocked it on 2026-09-29. Run it with `use_figma` once Pro is active.

**Design:**
- A 1920×960 frame filled with the brand firouzeh `#0b6264`, bound to the `primary` variable.
- Right side, right-aligned: «آبادین» at 220px ExtraBold, «دیزاین سیستم», a one-line tagline, and chips for the theme, shadcn/ui, the font and the version.
- Left side: a staircase of the real Spacing scale (۴ to ۶۴ px), with bottoms aligned on one baseline. It reads as construction steps built from the system's own tokens.
- The script sets the frame as the file thumbnail.

```js
const page=await figma.getNodeByIdAsync('0:1'); await figma.setCurrentPageAsync(page);
for (const s of ['Regular','Medium','SemiBold','ExtraBold']) await figma.loadFontAsync({family:'Vazirmatn',style:s});
const hex=h=>({r:parseInt(h.slice(1,3),16)/255,g:parseInt(h.slice(3,5),16)/255,b:parseInt(h.slice(5,7),16)/255});
const solid=h=>[{type:'SOLID',color:hex(h)}];
const primary=await figma.variables.getVariableByIdAsync('VariableID:2:45');
const W=1920,H=960;
const f=figma.createFrame(); f.name='Cover'; f.resize(W,H); f.x=0; f.y=0; f.clipsContent=true;
f.fills=[figma.variables.setBoundVariableForPaint({type:'SOLID',color:hex('#0b6264')},'color',primary)];
const ids=[f.id];
const steps=[4,8,12,16,20,24,32,40,48,64];
const fa=n=>String(n).replace(/\d/g,d=>'۰۱۲۳۴۵۶۷۸۹'[d]);
const base=H-160, unit=6.5, bw=64, gap=12; let x=120;
const cap=figma.createText(); cap.fontName={family:'Vazirmatn',style:'Medium'}; cap.fontSize=20; cap.lineHeight={unit:'PIXELS',value:28}; cap.characters='مقیاس فاصله‌گذاری · پیکسل'; cap.fills=solid('#76bdb9'); f.appendChild(cap); cap.x=120; cap.y=base+56; ids.push(cap.id);
steps.forEach((v,i)=>{
  const hgt=v*unit; const r=figma.createRectangle(); r.name=`step/${v}`; r.resize(bw,hgt); r.x=x; r.y=base-hgt;
  r.fills=solid(i%2? '#0a4f51':'#107270'); r.topLeftRadius=r.topRightRadius=4; f.appendChild(r); ids.push(r.id);
  const l=figma.createText(); l.fontName={family:'Vazirmatn',style:'Medium'}; l.fontSize=18; l.lineHeight={unit:'PIXELS',value:24}; l.characters=fa(v); l.fills=solid('#a9d8d5'); l.textAlignHorizontal='CENTER';
  f.appendChild(l); l.resize(bw,24); l.x=x; l.y=base+14; ids.push(l.id);
  x+=bw+gap;
});
const ruler=figma.createRectangle(); ruler.name='baseline'; ruler.resize(x-gap-120,2); ruler.x=120; ruler.y=base; ruler.fills=solid('#a9d8d5'); f.appendChild(ruler); ids.push(ruler.id);
const col=figma.createAutoLayout('VERTICAL',{name:'Identity',itemSpacing:8}); col.fills=[]; col.counterAxisAlignItems='MAX';
const t=(chars,style,size,lh,color)=>{ const n=figma.createText(); n.fontName={family:'Vazirmatn',style}; n.fontSize=size; n.lineHeight={unit:'PIXELS',value:lh}; n.characters=chars; n.fills=solid(color); n.textAlignHorizontal='RIGHT'; return n; };
for (const n of [t('Abadin · Design System','Medium',22,32,'#a9d8d5'),t('آبادین','ExtraBold',220,280,'#ffffff'),t('دیزاین سیستم','SemiBold',64,88,'#d3ecea'),t('مقایسهٔ قیمت مصالح ساختمانی، پیش از تماس با فروشنده','Regular',26,40,'#a9d8d5')]) col.appendChild(n);
f.appendChild(col); col.x=W-120-col.width; col.y=180; ids.push(col.id);
const meta=figma.createAutoLayout('HORIZONTAL',{name:'Meta',itemSpacing:12}); meta.fills=[];
for (const s of ['تم روشن','shadcn/ui','وزیرمتن','نسخهٔ ۰٫۱ · مهر ۱۴۰۵']){
  const chip=figma.createAutoLayout('HORIZONTAL',{name:'chip'}); chip.paddingLeft=chip.paddingRight=20; chip.paddingTop=chip.paddingBottom=10; chip.cornerRadius=999;
  chip.fills=[]; chip.strokes=solid('#46a09c'); chip.strokeWeight=1.5;
  chip.appendChild(t(s,'Medium',20,28,'#d3ecea')); meta.appendChild(chip);
}
f.appendChild(meta); meta.x=W-120-meta.width; meta.y=H-120-meta.height; ids.push(meta.id);
await figma.setFileThumbnailNodeAsync(f);
await f.screenshot({scale:0.5});
return {coverId:f.id, ids};
```
