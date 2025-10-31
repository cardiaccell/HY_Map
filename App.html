<!doctype html>
<html lang="ko">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>한양대학교 캠퍼스 맵 (웹 데모)</title>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" crossorigin/>
  <style>
    :root { --sidebar-w: 380px; }
    * { box-sizing: border-box; }
    body { margin:0; font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, "Apple SD Gothic Neo","Noto Sans KR","Malgun Gothic", sans-serif; }
    .wrap { display:grid; grid-template-columns: var(--sidebar-w) 1fr; min-height:100vh; }
    .sidebar { padding:16px; border-right:1px solid #e5e7eb; overflow-y:auto; }
    .sidebar h1 { font-size:18px; margin:0 0 8px; }
    .muted { color:#6b7280; font-size:12px; }
    .field { margin-top:12px; }
    .label { display:block; font-size:12px; color:#6b7280; margin-bottom:4px; }
    input, button { padding:8px 10px; border:1px solid #d1d5db; border-radius:8px; background:#fff; font-size:14px; }
    input[type="text"]{ width:100%; }
    button.primary{ background:#111827; color:#fff; border-color:#111827; cursor:pointer; }
    button.secondary{ background:#2563eb; color:#fff; border-color:#2563eb; cursor:pointer; }
    button.ghost{ background:#fff; color:#111827; border-color:#d1d5db; cursor:pointer; }
    .row{ display:flex; gap:8px; align-items:center; }
    .space-between{ justify-content:space-between; }
    .pill{ display:inline-block; padding:2px 8px; border-radius:999px; font-size:12px; border:1px solid #e5e7eb; background:#fafafa; }
    #map{ height:100vh; width:100%; }
    .badge{ display:inline-block; padding:2px 6px; font-size:11px; border-radius:6px; background:#eef2ff; color:#3730a3; }
    .photo{ width:240px; height:150px; background:#f3f4f6; border-radius:10px; overflow:hidden; display:flex; align-items:center; justify-content:center; color:#9ca3af; font-size:12px; }
    .legend{ display:flex; gap:8px; align-items:center; font-size:12px; color:#4b5563 }
    .chip{ width:16px; height:4px; border-radius:2px; }
    .steps{ margin-top:8px; display:grid; gap:6px; }
    .step{ display:flex; gap:8px; font-size:12px; color:#111827; }
    .step .d{ color:#6b7280; }
    .search-results{ border:1px solid #e5e7eb; border-radius:10px; padding:8px; margin-top:6px; max-height:180px; overflow:auto; }
    .search-item{ padding:6px; border-radius:8px; cursor:pointer; font-size:13px; }
    .search-item:hover{ background:#f3f4f6; }
    .toggle{ display:flex; gap:8px; align-items:center; }
    /* 포인터 & 빠른 로딩 효과 */
    .poi-hit{ cursor:pointer !important; }
    .skeleton{ background: linear-gradient(90deg,#f3f4f6 25%,#e5e7eb 37%,#f3f4f6 63%); background-size:400% 100%; animation: shimmer 1.2s infinite; }
    @keyframes shimmer{0%{background-position:100% 0}100%{background-position:-100% 0}}
  </style>
</head>
<body>
  <div class="wrap">
    <aside class="sidebar">
      <h1>한양대학교 캠퍼스 맵 (웹 데모 v7)</h1>

      <!-- 검색 -->
      <div class="field">
        <label class="label">검색(건물/시설명)</label>
        <div class="row">
          <input id="q" type="text" placeholder="예: 버거킹 동대문점 / 백남학술정보관" />
          <button id="btnSearch" class="secondary">검색</button>
        </div>
        <div id="searchResults" class="search-results" style="display:none"></div>
      </div>

      <!-- 요약/모드 -->
      <div class="field">
        <div class="row space-between">
          <span class="badge">경로 요약</span>
          <div class="legend">
            <div class="chip" style="background:#2563eb"></div><span>가장빠름</span>
            <div class="chip" style="background:#16a34a"></div><span>계단 회피</span>
          </div>
        </div>
        <div id="routeSummary" class="muted" style="margin-top:6px; font-size:16px; font-weight:700">출발·도착을 선택하세요.</div>
      </div>

      <div class="field row space-between">
        <span id="srcTag" class="pill" title="출발지">출발: -</span>
        <button id="clearSrc" class="ghost" style="width:auto">초기화</button>
      </div>
      <div class="field row space-between">
        <span id="dstTag" class="pill" title="도착지">도착: -</span>
        <button id="clearDst" class="ghost" style="width:auto">초기화</button>
      </div>

      <div class="field">
        <label class="label">경로 옵션</label>
        <div class="row">
          <label class="toggle"><input type="radio" name="mode" value="fast" checked> 가장빠른 길</label>
          <label class="toggle"><input type="radio" name="mode" value="accessible"> 계단 회피</label>
        </div>
      </div>

      <div class="field">
        <button id="locBtn" class="primary">내 위치 찾기</button>
        <p class="muted">위치 기능은 <b>HTTPS</b> 또는 <b>localhost</b>에서 동작.</p>
      </div>

      <div class="field">
        <h3 style="margin:8px 0 6px; font-size:14px">경로 상세</h3>
        <div id="steps" class="steps"></div>
      </div>
    </aside>
    <main><div id="map"></div></main>
  </div>

  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js" crossorigin></script>
  <script>
    const CAMPUS_BBOX = [127.0385, 37.5530, 127.0515, 37.5620];
    const CAMPUS_CENTER = { lat: 37.5577, lng: 127.0456 };
    const photoDB = { };

    // 지도
    const map = L.map('map').setView([CAMPUS_CENTER.lat, CAMPUS_CENTER.lng], 16);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', { maxZoom:20, attribution:'&copy; OpenStreetMap' }).addTo(map);
    // POI 표시 레이어
    const poiLayer = L.layerGroup().addTo(map);

    // 상태
    let source=null, target=null;
    let routeLayer=null, userMarker=null, srcHighlight=null, dstHighlight=null, facilityMarker=null;
    let currentMode='fast';

    // DOM
    const routeSummary = document.getElementById('routeSummary');
    const srcTag = document.getElementById('srcTag');
    const dstTag = document.getElementById('dstTag');
    const stepsEl = document.getElementById('steps');

    document.getElementById('clearSrc').onclick = ()=>{ source=null; updateTags(); draw(); };
    document.getElementById('clearDst').onclick = ()=>{ target=null; updateTags(); draw(); };
    document.querySelectorAll('input[name="mode"]').forEach(r=> r.addEventListener('change', ()=>{ currentMode = document.querySelector('input[name="mode"]:checked').value; draw(); }));
    document.getElementById('locBtn').onclick = ()=>{
      if (!navigator.geolocation) return alert('이 브라우저는 위치 기능을 지원하지 않습니다.');
      const btn = document.getElementById('locBtn'); btn.disabled=true; btn.textContent='내 위치 찾는 중...';
      navigator.geolocation.getCurrentPosition(p=>{
        const {latitude, longitude}=p.coords;
        if (userMarker) userMarker.remove();
        userMarker = L.marker([latitude, longitude]).addTo(map).bindPopup('내 위치');
        map.flyTo([latitude, longitude], 17, {duration:0.6});
        btn.disabled=false; btn.textContent='내 위치 찾기';
      }, _=>{ alert('위치 권한을 허용해주세요.'); btn.disabled=false; btn.textContent='내 위치 찾기'; }, {enableHighAccuracy:true, timeout:8000, maximumAge:2000});
    };

    // 검색
    const q = document.getElementById('q'); const btnSearch = document.getElementById('btnSearch'); const searchResults = document.getElementById('searchResults');
    btnSearch.onclick = doSearch; q.addEventListener('keydown', e=>{ if (e.key==='Enter') doSearch(); });
    async function doSearch(){
      const text = q.value.trim(); if (!text) return;
      const url = `https://nominatim.openstreetmap.org/search?format=jsonv2&q=${encodeURIComponent(text)}&bounded=1&viewbox=${CAMPUS_BBOX.join(',')}&accept-language=ko`;
      const res = await fetch(url, {headers:{'Accept':'application/json'}}); const data = await res.json(); renderSearch(data);
    }
    function renderSearch(items){
      if (!items || items.length===0){ searchResults.style.display='none'; searchResults.innerHTML=''; return; }
      searchResults.style.display='block'; searchResults.innerHTML='';
      items.slice(0,12).forEach(it=>{
        const div = document.createElement('div'); div.className='search-item'; div.textContent = it.display_name;
        div.onclick = ()=>{ const lat=parseFloat(it.lat), lon=parseFloat(it.lon); openPlacePopupFast(lat, lon, it.display_name); map.flyTo([lat,lon], 18, {duration:0.3}); };
        searchResults.appendChild(div);
      });
    }

    // 지도 클릭(POI가 아닐 때)
    map.on('click', async (e)=>{
      const {lat,lng}=e.latlng;
      const place = await reverseGeocode(lat, lng);
      openPlacePopupFast(lat, lng, place?.display_name || `${lat.toFixed(5)}, ${lng.toFixed(5)}`);
    });

    // ===== 빠른 팝업(사진은 비동기) =====
    async function openPlacePopupFast(lat, lng, label){
      if (facilityMarker) { facilityMarker.remove(); facilityMarker=null; }
      facilityMarker = L.marker([lat,lng]).addTo(map);
      const baseHtml = `
        <div style="font-size:13px">
          <div class="photo skeleton" id="ph">사진 불러오는 중...</div>
          <div style="margin-top:8px; font-weight:600">${label}</div>
          <div class="muted">접근성: Ex(양호), 혼잡도: Ex(68%)</div>
          <div style="display:flex; gap:6px; margin-top:8px">
            <button class="primary" style="width:auto" onclick='window._setSrc(${lat},${lng},${JSON.stringify(label)})'>출발</button>
            <button class="secondary" style="width:auto" onclick='window._setDst(${lat},${lng},${JSON.stringify(label)})'>도착</button>
          </div>
        </div>`;
      const pop = L.popup().setLatLng([lat,lng]).setContent(baseHtml).openOn(map);
      setTimeout(async ()=>{
        const photo = await findPhoto(label);
        const container = pop.getElement(); if (!container) return;
        const ph = container.querySelector('#ph'); if (!ph) return;
        ph.innerHTML = photo ? `<img src="${photo}" style="width:100%;height:100%;object-fit:cover"/>` : '사진 없음';
        ph.classList.remove('skeleton');
      }, 0);
    }

    // 전역 setter
    window._setSrc = (lat,lng,label)=>{ source={lat,lng,label}; updateTags(); draw(); map.closePopup(); };
    window._setDst = (lat,lng,label)=>{ target={lat,lng,label}; updateTags(); draw(); map.closePopup(); };
    function updateTags(){ srcTag.textContent = `출발: ${source? '선택됨' : '-'}`; dstTag.textContent = `도착: ${target? '선택됨' : '-'}`; }

    // 라우팅
    async function draw(){
      if (routeLayer){ routeLayer.remove(); routeLayer=null; }
      stepsEl.innerHTML=''; clearHighlights();

      if (source){ srcHighlight = L.circleMarker([source.lat,source.lng], {radius:12, color:'#111827', weight:3, fillOpacity:0}).addTo(map); }
      if (target){ dstHighlight = L.circleMarker([target.lat,target.lng], {radius:12, color:(currentMode==='fast'?'#2563eb':'#16a34a'), weight:3, fillOpacity:0}).addTo(map); }
      if (!(source && target)){ routeSummary.textContent='출발·도착을 선택하세요.'; return; }

      if (currentMode==='fast'){
        const r = await osrmWalkRoute([source.lng,source.lat],[target.lng,target.lat]);
        if (!r){ routeSummary.textContent='경로를 찾지 못했습니다.'; return; }
        const coords = r.geometry.coordinates.map(c=>[c[1],c[0]]);
        const start = coords[0], end = coords[coords.length-1];
        const stitched = [];
        stitched.push([source.lat,source.lng]);
        if (hav(source.lat,source.lng,start[0],start[1])>1) stitched.push(start);
        coords.slice(1,-1).forEach(pt=>stitched.push(pt));
        if (hav(end[0],end[1],target.lat,target.lng)>1) stitched.push(end);
        stitched.push([target.lat,target.lng]);
        routeLayer = L.polyline(stitched, {color:'#2563eb', weight:5}).addTo(map);
        const extra = hav(source.lat,source.lng,start[0],start[1]) + hav(end[0],end[1],target.lat,target.lng);
        const totalDist = r.distance + extra;
        const totalDur  = r.duration + extra/1.3;
        routeSummary.textContent = `거리 ${fmtDistance(totalDist)} · 도보 ${fmtMin(totalDur)}`;
        renderSteps(r.steps);
        map.fitBounds(routeLayer.getBounds(), {padding:[40,40]});
      } else {
        const g = campusGraph();
        const path = aStar(g, {lon:source.lng,lat:source.lat}, {lon:target.lng,lat:target.lat}, {avoidStairs:true});
        if (!path){ routeSummary.textContent='경로를 찾지 못했습니다.'; return; }
        const coords = path.map(p=>[p.lat,p.lon]);
        const stitched = [[source.lat,source.lng], ...coords, [target.lat,target.lng]];
        routeLayer = L.polyline(stitched, {color:'#16a34a', weight:5}).addTo(map);
        const dist = pathDistance(stitched);
        routeSummary.textContent = `거리 ${fmtDistance(dist)} · 도보 ${fmtMin(dist/1.3)}`;
        renderSteps(polylineToSteps(stitched));
        map.fitBounds(routeLayer.getBounds(), {padding:[40,40]});
      }
    }
    function clearHighlights(){ if (srcHighlight){srcHighlight.remove();srcHighlight=null;} if (dstHighlight){dstHighlight.remove();dstHighlight=null;} }
    function fmtDistance(m){ return m<1000 ? `${Math.round(m)} m` : `${(m/1000).toFixed(2)} km`; }
    function fmtMin(sec){ const m = Math.max(1, Math.round(sec/60)); return `${m}분`; }
    function renderSteps(steps){ stepsEl.innerHTML=''; (steps||[]).forEach((s,i)=>{ const d=document.createElement('div'); d.className='step'; d.innerHTML=`<div>${i+1}.</div><div>${s.instruction||s.text||'이동'}</div><div class='d'>${s.distance?fmtDistance(s.distance):''}</div>`; stepsEl.appendChild(d); }); }

    // OSRM
    async function osrmWalkRoute([lon1,lat1],[lon2,lat2]){
      try{
        const base='https://router.project-osrm.org/route/v1/foot/';
        const url = `${base}${lon1},${lat1};${lon2},${lat2}?overview=full&geometries=geojson&alternatives=false&steps=true&annotations=distance`;
        const res = await fetch(url); if (!res.ok) return null;
        const j = await res.json(); const r=j?.routes?.[0]; if (!r) return null;
        const steps = (r.legs||[]).flatMap(leg => (leg.steps||[]).map(st => ({instruction: st.maneuver?.instruction || st.name || '이동', distance: st.distance})));
        return {distance:r.distance, duration:r.duration, geometry:r.geometry, steps};
      }catch{ return null; }
    }

    // 지오코딩/사진
    async function reverseGeocode(lat, lon){
      try{ const url = `https://nominatim.openstreetmap.org/reverse?lat=${lat}&lon=${lon}&format=jsonv2&zoom=18&addressdetails=1&accept-language=ko`; const r = await fetch(url); if (!r.ok) return null; return r.json(); }catch{ return null; }
    }
    async function findPhoto(label){
      if (photoDB[label]) return photoDB[label];
      const controller = new AbortController(); const t=setTimeout(()=>controller.abort(), 1200);
      try{ const api = `https://en.wikipedia.org/w/api.php?action=query&prop=pageimages|images&format=json&origin=*&piprop=thumbnail&pithumbsize=600&titles=${encodeURIComponent(label)}`; const r=await fetch(api,{signal:controller.signal}); clearTimeout(t); if(!r.ok) return null; const j=await r.json(); const pages=j.query?.pages||{}; const first=Object.values(pages)[0]; return first?.thumbnail?.source || null; }catch{ return null; }
    }

    // 데모 그래프(A*)
    function campusGraph(){
      const nodes = [
        {id:'gate', lon:127.0449, lat:37.5579},
        {id:'plaza', lon:127.0456, lat:37.5585},
        {id:'lib', lon:127.0447, lat:37.55734},
        {id:'eng', lon:127.0482, lat:37.5564},
        {id:'stu', lon:127.0467, lat:37.55927},
        {id:'caf', lon:127.0453, lat:37.55978},
      ];
      const byId = Object.fromEntries(nodes.map(n=>[n.id,n]));
      const E=[]; const add=(a,b,opts={})=>{ const n1=byId[a], n2=byId[b]; const d=hav(n1.lat,n1.lon,n2.lat,n2.lon); const cost = d*(opts.stairs?3:1)*(opts.elevator?0.8:1); E.push({a,b,d,stairs:!!opts.stairs,elevator:!!opts.elevator,cost}); E.push({a:b,b:a,d,stairs:!!opts.stairs,elevator:!!opts.elevator,cost}); };
      add('gate','plaza'); add('plaza','lib'); add('plaza','stu'); add('plaza','eng',{stairs:true}); add('plaza','caf');
      return {nodes, edges:E, byId};
    }
    function nearestNode(g,p){ let best=null, bestD=1e9; for(const n of g.nodes){ const d=hav(p.lat,p.lon,n.lat,n.lon); if(d<bestD){best=n; bestD=d;} } return best; }
    function aStar(g,s,t,opt={}){ const start=nearestNode(g,s), goal=nearestNode(g,t); const open=new Set([start.id]); const came={}, gS={}, fS={}; g.nodes.forEach(n=>{gS[n.id]=Infinity; fS[n.id]=Infinity;}); gS[start.id]=0; fS[start.id]=hav(start.lat,start.lon,goal.lat,goal.lon);
      while(open.size){ let cur=null,cf=Infinity; open.forEach(id=>{ if(fS[id]<cf){cf=fS[id]; cur=id;} }); if(cur===goal.id) return reconstruct(came,g.byId,cur);
        open.delete(cur);
        for(const e of g.edges.filter(e=>e.a===cur)){ if(opt.avoidStairs && e.stairs) continue; const tentative=gS[cur]+e.cost; if(tentative<gS[e.b]){ came[e.b]=cur; gS[e.b]=tentative; const nb=g.byId[e.b]; fS[e.b]=tentative+hav(nb.lat,nb.lon,goal.lat,goal.lon); open.add(e.b);} }
      } return null; }
    function reconstruct(came,byId,cur){ const path=[byId[cur]]; while(came[cur]){ cur=came[cur]; path.push(byId[cur]); } return path.reverse(); }
    function polylineToSteps(coords){ const steps=[]; for(let i=1;i<coords.length;i++){ const a=coords[i-1], b=coords[i]; steps.push({text:'이동', distance: hav(a[0],a[1],b[0],b[1])}); } return steps; }
    function pathDistance(coords){ let s=0; for(let i=1;i<coords.length;i++){ s+=hav(coords[i-1][0],coords[i-1][1],coords[i][0],coords[i][1]); } return s; }
    function hav(lat1,lon1,lat2,lon2){ const R=6371000, toR=x=>x*Math.PI/180; const dLat=toR(lat2-lat1), dLon=toR(lon2-lon1); const a=Math.sin(dLat/2)**2 + Math.cos(toR(lat1))*Math.cos(toR(lat2))*Math.sin(dLon/2)**2; return 2*R*Math.atan2(Math.sqrt(a),Math.sqrt(1-a)); }

    // ===== 전 시설(모든 이름 있는 객체) 미리 로드: Overpass =====
    async function preloadPOIs(){
      try{
        const [minLon,minLat,maxLon,maxLat] = CAMPUS_BBOX;
        // 이름이 있는 모든 객체(node/way/relation)를 로드 (캠퍼스 bbox 한정)
        const overpass = `[out:json][timeout:25];(nwr[\"name\"](${minLat},${minLon},${maxLat},${maxLon}););out center;`;
        const q = `https://overpass-api.de/api/interpreter?data=${encodeURIComponent(overpass)}`;
        const r = await fetch(q);
        if (!r.ok) return;
        const j = await r.json();
        const seen = new Set();
        const feats = (j.elements||[])
          .map(el=>({ id: el.id, lat: el.lat || el.center?.lat, lon: el.lon || el.center?.lon, tags: el.tags||{} }))
          .filter(f=>f.lat && f.lon && f.tags.name)
          .map(f=>({ id:f.id, lat:f.lat, lon:f.lon, name: f.tags['name:ko']||f.tags.name, cat: guessCategory(f.tags) }));

        feats.forEach(f=>{
          const key = `${f.lat.toFixed(6)},${f.lon.toFixed(6)}`; if (seen.has(key)) return; seen.add(key);
          // 넉넉한 히트존으로 '모든 시설' 포인터 처리
          const m = L.circleMarker([f.lat,f.lon], { radius: 18, opacity:0, fillOpacity:0, className:'poi-hit' }).addTo(poiLayer);
          m.on('mouseover', ()=>{ map.getContainer().style.cursor='pointer'; });
          m.on('mouseout', ()=>{ map.getContainer().style.cursor=''; });
          m.on('click', ()=>{ openPlacePopupFast(f.lat, f.lon, f.name || f.cat || '장소'); map.flyTo([f.lat,f.lon], 18, {duration:0.2}); });
          m.bindTooltip(f.name || '장소', {permanent:false, direction:'top'});
        });
      }catch(e){ /* ignore */ }
    }
    function guessCategory(tags){
      return tags.amenity || tags.shop || tags.building || tags.tourism || tags.leisure || tags.healthcare || tags.office || 'place';
    }
    preloadPOIs();
  </script>
</body>
</html>
