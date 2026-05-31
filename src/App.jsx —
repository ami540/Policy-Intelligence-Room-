import { useState, useRef } from "react";

const C = {
  bg:"#080c0e",surface:"#0d1416",card:"#111820",border:"#1c2a30",
  green:"#00e5a0",greenDim:"#00b87a",greenFaint:"#00e5a015",
  amber:"#f5a623",red:"#e05252",blue:"#4a9eff",purple:"#9b6dff",
  textPrimary:"#e8edf0",textSecondary:"#7a9aaa",textMuted:"#4a6070",
};
const mono="'Courier New','Lucida Console',monospace";
const sans="'DM Sans','Segoe UI',system-ui,sans-serif";
const display="'Georgia','Times New Roman',serif";

const SAMPLE = {
  meta:{
    title:"Canadian Charitable Tax Incentive Reform: Federal Policy Analysis",
    type:"Policy Research Brief",jurisdiction:"Canada · Federal",
    date:"2024-09-01",pages:42,wordCount:"18,600",
    classification:"PUBLIC",analyst:"Policy Room Intelligence",
    riskScore:38,completeness:91,confidence:85,dataCoverage:"High",
    missingInfo:[
      "CRA administrative cost estimates not publicly available",
      "Provincial revenue impact data incomplete for AB and SK",
      "Donor behavioural response modelling based on U.S. proxies",
    ],
    researchBacked:true,
  },
  executive:`Canada's charitable tax credit system has not been substantially reformed since 1988, creating structural inefficiencies that disproportionately benefit high-income donors while failing to stimulate giving among middle-income Canadians. Current credits provide an after-tax cost of roughly $0.46 per dollar donated at the top marginal rate versus $0.79 for lower-bracket donors. This is a regressive incentive architecture that contradicts stated equity objectives. The price elasticity of Canadian charitable giving is estimated at -1.1, meaning incentive design has measurable effects on donor behaviour. Three reform models have been assessed, including a flat federal credit, a UK-style matched-giving scheme, and a graduated civic dividend for first-time donors. All are likely to expand total charitable giving and partially offset fiscal cost, though the magnitude of behavioural response remains uncertain.`,
  issues:[
    {id:1,title:"Regressive Credit Architecture",severity:"critical",tags:["Equity","Tax Policy"],summary:"Top-bracket donors receive a 72% larger effective subsidy per dollar donated than middle-income Canadians. A $1,000 gift costs a high-income donor roughly $460 after tax versus $790 for a middle-income donor. Participation rate has fallen from 30% in 1990 to 24% in 2007 as giving concentrates upward."},
    {id:2,title:"Stagnant Middle-Income Giving",severity:"high",tags:["Behavioural","Revenue"],summary:"Participation rates among Canadians earning $50K to $100K have fallen substantially since 2007. This is a trend the current credit structure likely exacerbates. Price elasticity data suggests targeted credit enhancement would likely reverse this decline."},
    {id:3,title:"Sector Concentration Risk",severity:"high",tags:["Sector","Distribution"],summary:"A significant majority of donated dollars flow to religious organizations and hospitals, while arts, environment, and social services remain systematically underfunded relative to public benefit generated."},
    {id:4,title:"Foundation Payout Inefficiency",severity:"high",tags:["Foundations","Fiscal"],summary:"Private foundations receive immediate and substantial tax relief but are only required to disburse a small minimum annually. Alepin (2020) argues this creates effective warehousing of tax-subsidized assets. In some cases this deferral is indefinite."},
    {id:5,title:"First-Time Donor Super Credit Sunset",severity:"medium",tags:["Policy Gap","Participation"],summary:"The First-Time Donor Super Credit (2013 to 2017) produced measurable uptake effects among new donors but was allowed to lapse without formal evaluation. The evidence base for re-introduction is strong and fiscally modest."},
  ],
  stakeholders:[
    {name:"Canada Revenue Agency",role:"Regulatory Authority",influence:90,position:"mixed",notes:"Supports simplification. Concerned about administrative cost of matched-giving model. Flat credit administratively preferable.",group:"regulator"},
    {name:"Imagine Canada",role:"Sector Advocacy",influence:78,position:"supportive",notes:"Strongly supports flat credit and matched-giving models. Has lobbied consistently since 2019. Broad coalition capacity.",group:"ngo"},
    {name:"Finance Canada",role:"Federal Ministry",influence:95,position:"mixed",notes:"Receptive to cost-neutral options. Resistant to proposals exceeding $250M net annual cost without behavioural offset modelling.",group:"government"},
    {name:"High-Income Donors",role:"Donor Class",influence:65,position:"opposed",notes:"Any credit flattening reduces the effective subsidy at top rates. Organized resistance through Philanthropic Foundations Canada.",group:"industry"},
    {name:"Community Foundations",role:"Intermediary Sector",influence:60,position:"supportive",notes:"Supports reforms that expand donor pool. Particularly interested in community-directed giving and matched models.",group:"ngo"},
    {name:"Religious Organizations",role:"Beneficiary Sector",influence:72,position:"mixed",notes:"Largest recipient sector. Neutral on reform but monitoring concentration-risk provisions closely.",group:"citizens"},
  ],
  influenceLinks:[
    {source:"Imagine Canada",target:"Finance Canada",strength:0.7,type:"align"},
    {source:"Community Foundations",target:"Imagine Canada",strength:0.85,type:"align"},
    {source:"High-Income Donors",target:"Finance Canada",strength:0.75,type:"conflict"},
    {source:"Canada Revenue Agency",target:"Finance Canada",strength:0.8,type:"align"},
    {source:"High-Income Donors",target:"Imagine Canada",strength:0.6,type:"conflict"},
    {source:"Religious Organizations",target:"Finance Canada",strength:0.5,type:"align"},
    {source:"Community Foundations",target:"Canada Revenue Agency",strength:0.4,type:"align"},
  ],
  winnersLosers:{
    winners:[
      {actor:"Middle-income donors ($50K to $100K)",reason:"Flat credit model meaningfully raises effective incentive rate for this bracket. This represents a direct reversal of the documented participation decline."},
      {actor:"Small and community-based charities",reason:"A broader, more distributed donor base is likely to reduce sector concentration."},
      {actor:"Imagine Canada and sector advocates",reason:"Reform would validate a sustained advocacy campaign and strengthen the sector's credibility with Finance Canada."},
      {actor:"First-time and young donors",reason:"Front-loaded incentive structures are specifically designed to address the participation rate decline. This is a policy gap with strong evidence support."},
    ],
    losers:[
      {actor:"High-income donors and family foundations",reason:"Credit flattening reduces the effective subsidy at top marginal rates. Foundation payout reform would further constrain asset warehousing."},
      {actor:"Large religious and hospital foundations",reason:"A more distributed giving base is likely to shift charitable dollars away from the most concentrated institutional recipients."},
      {actor:"Tax planning industry",reason:"Credit simplification reduces the fee-generating complexity of charitable giving strategies, particularly around capital gains."},
      {actor:"Finance Canada (short-term)",reason:"Net fiscal cost is meaningful before behavioural offsets are realized. Likely three or more years before offsets materialize."},
    ],
  },
  risks:[
    {category:"Political Feasibility",score:35,label:"MODERATE",detail:"Cross-partisan support exists in principle. Cost optics during fiscal consolidation are the primary constraint. Not ideological opposition.",color:"#00b87a"},
    {category:"Revenue Uncertainty",score:52,label:"ELEVATED",detail:"Behavioural response to credit reform is measurable but uncertain. If uptake is weaker than elasticity projections suggest, net cost could be substantially higher.",color:"#f5a623"},
    {category:"Donor Lobby Opposition",score:38,label:"MODERATE",detail:"High-income donor organizations have demonstrated capacity to delay reform through counter-research and coordinated opposition. Risk is real but manageable.",color:"#00b87a"},
    {category:"CRA Implementation",score:45,label:"MODERATE",detail:"The flat credit model is administratively straightforward. A matched-giving scheme would require new CRA infrastructure. Implementation risk is concentrated in second-phase options.",color:"#00b87a"},
    {category:"Provincial Harmonization",score:58,label:"ELEVATED",detail:"Quebec and Alberta have signalled divergent preferences. Federal reform without bilateral pre-consultation is likely to produce a patchwork system and significant political friction.",color:"#f5a623"},
  ],
  economic:{
    gdpImpact:"Likely modest positive",
    complianceCost:"Estimated $180M to $340M annually (net federal, pre-offset). Uncertainty is high.",
    sectorImpact:[
      {sector:"Social Services Charities",impact:"positive",magnitude:4},
      {sector:"Arts and Culture",impact:"positive",magnitude:4},
      {sector:"Environmental Organizations",impact:"positive",magnitude:3},
      {sector:"Religious Organizations",impact:"neutral",magnitude:2},
      {sector:"Large Hospital Foundations",impact:"negative",magnitude:2},
      {sector:"Tax Planning Industry",impact:"negative",magnitude:3},
    ],
  },
  ministerBrief:{
    issue:"Federal charitable tax credit reform. Structural overhaul of Canada's donor incentive system to address a documented regressive design.",
    whatHappened:`Canada's charitable giving tax credit has remained structurally unchanged since 1988. Original research demonstrates the current two-tier federal credit creates a regressive incentive where high-income donors receive a substantially larger effective subsidy per dollar donated than middle-income Canadians. Participation rates among middle-income households have declined materially since 2007.\n\nThree reform models have been assessed: a flat federal credit with the lowest administrative burden, a UK-style matched-giving scheme with the highest participation effect but significant CRA infrastructure requirements, and a graduated civic dividend targeting first-time donors with the lowest fiscal cost. All are expected to increase total charitable giving and partially offset fiscal cost over time, though the behavioural response is inherently uncertain.`,
    politicalRisk:"MODERATE",
    politicalRiskDetail:"Cross-partisan support exists. Primary risk is cost framing during fiscal consolidation. Manageable with pre-emptive behavioural offset modelling.",
    mediaRisk:"LOW",
    mediaRiskDetail:"Charitable reform is broadly popular. Vulnerability concentrated in opposition framing around reduced benefits for wealthy donors. Addressable through equity messaging.",
    recommendedPosition:"SUPPORT WITH AMENDMENTS",
    recommendedPositionDetail:"Endorse the flat federal credit as the lowest-cost, highest-impact option. Pair with a time-limited first-time donor incentive with mandatory evaluation. Require provincial pre-consultation before tabling.",
  },
  mediaNarrative:{
    industryReaction:"Business community broadly neutral. Tax planning firms will oppose simplification through professional associations. Expect quiet lobbying rather than public opposition. Philanthropic Foundations Canada is likely to commission counter-research within weeks of any announcement.",
    oppositionReaction:"NDP will support if equity provisions are central and will attack any version maintaining higher benefits for top-bracket donors. CPC likely supportive of a flat credit, framing it as reducing complexity. Bloc Quebecois will monitor Quebec credit harmonization and may use as a regional differentiation issue.",
    probableHeadline:'"Ottawa overhauls 35-year-old charity tax rules, shifting breaks toward middle-class donors"',
    secondaryHeadline:'"Wealthy donors, family foundations face reduced tax advantages under proposed credit reform"',
    emergingCoalition:"A broad civil society coalition is likely to form including Imagine Canada, Community Foundations of Canada, United Way, and environment and arts sector organizations. The sector has demonstrated coordinated advocacy capacity in prior reform debates.",
    narrativeRisk:"The primary vulnerability is the gross cost frame. Opposition and media will anchor on the high end of fiscal cost estimates and are unlikely to foreground behavioural offsets without active communications work. Recommend pre-emptive release of Department of Finance cost-benefit modelling.",
  },
  recommendations:[
    {priority:"IMMEDIATE",action:"Release independent cost-benefit analysis of the flat credit model using Canadian donor panel data and published elasticity estimates to pre-empt opposition framing around gross fiscal cost."},
    {priority:"IMMEDIATE",action:"Initiate bilateral consultation with Quebec and Alberta finance ministries on harmonization before federal tabling. This is the most likely source of political friction if skipped."},
    {priority:"SHORT-TERM",action:"Re-introduce the First-Time Donor Super Credit as a time-limited complement to flat credit reform, with a mandatory evaluation trigger. The evidence base from its prior run (2013 to 2017) is credible and the fiscal exposure is modest."},
    {priority:"SHORT-TERM",action:"Anchor communications to an equity frame. The disparity in effective subsidy between income brackets is the most compelling and accessible argument for reform."},
    {priority:"MEDIUM-TERM",action:"Raise the private foundation annual payout quota from its current minimum toward a higher threshold to activate dormant tax-subsidized assets for active charitable use."},
    {priority:"ONGOING",action:"Monitor charitable sector giving data and participation rates via CRA. Validate behavioural uptake against elasticity projections at 12 and 36 month intervals, with a public evaluation commitment."},
  ],
  jurisdictions:[
    {name:"United Kingdom",framework:"Gift Aid",alignment:82,notes:"Matched-giving model is the direct comparator. 25-year track record of expanding donor base across income levels."},
    {name:"United States",framework:"Schedule A Deduction",alignment:45,notes:"Deduction model strongly favours high-income donors. This is the structural problem Canada is attempting to correct."},
    {name:"Australia",framework:"Deductible Gift Recipient",alignment:60,notes:"DGR framework provides useful precedent for sector eligibility and payout reform."},
    {name:"France",framework:"Flat Tax Credit (66 to 75 percent)",alignment:72,notes:"High flat credit rate demonstrates feasibility at scale. France recorded a 20% giving increase post-reform."},
    {name:"Quebec",framework:"Provincial Credit (20 plus 24 percent)",alignment:38,notes:"Quebec's independent credit system is the largest harmonization challenge. Divergent reform trajectory likely without bilateral pre-consultation."},
  ],
};

const DEMOS=[
  {label:"BC Clean Energy Regulation Review",type:"Regulatory Filing",tag:"Energy"},
  {label:"Federal Budget 2024 to 25 Analysis",type:"Budget Paper",tag:"Fiscal Policy"},
  {label:"National Housing Strategy Review",type:"Policy Report",tag:"Housing"},
  {label:"Bill C-27 Digital Charter Act",type:"Federal Legislation",tag:"AI Policy"},
];

function Tag({label,color="#4a6070",bg="#1c2a30"}){
  return <span style={{fontSize:10,fontFamily:mono,letterSpacing:"0.08em",color,background:bg,border:`1px solid ${color}30`,padding:"2px 7px",borderRadius:2,textTransform:"uppercase",fontWeight:700,whiteSpace:"nowrap"}}>{label}</span>;
}
function RiskBar({score,color}){
  return(
    <div style={{display:"flex",alignItems:"center",gap:10}}>
      <div style={{flex:1,height:4,background:"#1c2a30",borderRadius:2,overflow:"hidden"}}>
        <div style={{width:`${score}%`,height:"100%",background:color,borderRadius:2}}/>
      </div>
      <span style={{fontFamily:mono,fontSize:11,color,minWidth:28,textAlign:"right"}}>{score}</span>
    </div>
  );
}
function Card({children,style={}}){
  return <div style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px",...style}}>{children}</div>;
}
function SL({children}){
  return(
    <div style={{fontFamily:mono,fontSize:10,letterSpacing:"0.15em",color:C.green,textTransform:"uppercase",marginBottom:14,display:"flex",alignItems:"center",gap:8}}>
      <div style={{width:16,height:1,background:C.green}}/>
      {children}
      <div style={{flex:1,height:1,background:C.border}}/>
    </div>
  );
}
function SB({level}){
  const m={critical:{color:C.red,label:"CRITICAL"},high:{color:C.amber,label:"HIGH"},medium:{color:C.blue,label:"MEDIUM"},low:{color:C.textMuted,label:"LOW"}};
  const {color,label}=m[level]||m.low;
  return <Tag label={label} color={color} bg={color+"18"}/>;
}

function InfluenceMap({stakeholders,links,compact=false}){
  const W=640,H=compact?260:380;
  const groups={government:C.blue,industry:C.amber,ngo:C.purple,regulator:C.green,citizens:C.textSecondary};
  const n=stakeholders.length;
  const cx=W/2,cy=H/2,rx=W*0.36,ry=H*0.38;
  const pos=(i)=>({x:Math.round(cx+rx*Math.cos((2*Math.PI*i/n)-Math.PI/2)),y:Math.round(cy+ry*Math.sin((2*Math.PI*i/n)-Math.PI/2))});
  const pm={};
  stakeholders.forEach((s,i)=>{pm[s.name]=pos(i);});
  const gp=(name)=>pm[name]||{x:cx,y:cy};
  return(
    <div>
      <svg width="100%" viewBox={`0 0 ${W} ${H}`} style={{overflow:"visible",display:"block"}}>
        <defs>
          <marker id="aa" markerWidth="5" markerHeight="5" refX="4" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#00e5a0a0"/></marker>
          <marker id="ac" markerWidth="5" markerHeight="5" refX="4" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#e05252a0"/></marker>
          <filter id="gw"><feGaussianBlur stdDeviation="2.5" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
        </defs>
        {links&&links.map((lk,i)=>{
          const s=gp(lk.source),t=gp(lk.target);
          const dx=t.x-s.x,dy=t.y-s.y,len=Math.sqrt(dx*dx+dy*dy)||1;
          const pad=16+(stakeholders.find(x=>x.name===lk.source)?.influence||50)/100*10;
          const nx=dx/len*pad,ny=dy/len*pad;
          const col=lk.type==="align"?C.green:C.red;
          return(<line key={i} x1={s.x+nx} y1={s.y+ny} x2={t.x-nx} y2={t.y-ny} stroke={col} strokeOpacity={0.25+lk.strength*0.4} strokeWidth={lk.strength*2.2} strokeDasharray={lk.type==="conflict"?"5 3":"none"} markerEnd={`url(#${lk.type==="align"?"aa":"ac"})`}/>);
        })}
        {stakeholders.map((s,i)=>{
          const p=gp(s.name);
          const col=groups[s.group]||C.textMuted;
          const r=11+(s.influence/100)*13;
          const words=s.name.split(" ");
          const mid=Math.ceil(words.length/2);
          return(
            <g key={i}>
              <circle cx={p.x} cy={p.y} r={r+8} fill={col} opacity={0.07}/>
              <circle cx={p.x} cy={p.y} r={r} fill={C.card} stroke={col} strokeWidth={1.5} filter="url(#gw)"/>
              <text x={p.x} y={p.y+4} textAnchor="middle" fill={col} fontSize={8} fontFamily={mono} fontWeight="700">{s.influence}</text>
              <text x={p.x} y={p.y+r+13} textAnchor="middle" fill={C.textSecondary} fontSize={compact?8:9} fontFamily={sans}>{words.slice(0,mid).join(" ")}</text>
              {words.length>mid&&<text x={p.x} y={p.y+r+24} textAnchor="middle" fill={C.textSecondary} fontSize={compact?8:9} fontFamily={sans}>{words.slice(mid).join(" ")}</text>}
            </g>
          );
        })}
      </svg>
      {!compact&&(
        <div style={{display:"flex",gap:14,flexWrap:"wrap",marginTop:10}}>
          {[["government",C.blue,"GOVERNMENT"],["industry",C.amber,"INDUSTRY"],["ngo",C.purple,"NGO"],["regulator",C.green,"REGULATOR"],["citizens",C.textSecondary,"CIVIL SOCIETY"]].map(([k,col,lbl])=>(
            <div key={k} style={{display:"flex",alignItems:"center",gap:5}}>
              <div style={{width:7,height:7,borderRadius:"50%",background:col}}/>
              <span style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.08em"}}>{lbl}</span>
            </div>
          ))}
          <div style={{display:"flex",alignItems:"center",gap:5}}><svg width="16" height="5"><line x1="0" y1="2.5" x2="16" y2="2.5" stroke={C.green} strokeWidth="1.5"/></svg><span style={{fontFamily:mono,fontSize:9,color:C.textMuted}}>ALIGN</span></div>
          <div style={{display:"flex",alignItems:"center",gap:5}}><svg width="16" height="5"><line x1="0" y1="2.5" x2="16" y2="2.5" stroke={C.red} strokeWidth="1.5" strokeDasharray="4 2"/></svg><span style={{fontFamily:mono,fontSize:9,color:C.textMuted}}>CONFLICT</span></div>
        </div>
      )}
    </div>
  );
}

function TopBar({view,setView}){
  const nav=[{id:"landing",label:"HOME"},{id:"upload",label:"UPLOAD"},{id:"dashboard",label:"ANALYSIS"},{id:"brief",label:"BRIEFING"}];
  return(
    <div style={{position:"fixed",top:0,left:0,right:0,zIndex:100,background:C.bg+"f0",backdropFilter:"blur(10px)",borderBottom:`1px solid ${C.border}`,display:"flex",alignItems:"center",height:52,padding:"0 32px"}}>
      <div style={{display:"flex",alignItems:"center",gap:10,marginRight:48,cursor:"pointer"}} onClick={()=>setView("landing")}>
        <div style={{width:26,height:26,border:`1.5px solid ${C.green}`,display:"flex",alignItems:"center",justifyContent:"center",position:"relative"}}>
          <div style={{width:10,height:10,background:C.green}}/>
          <div style={{position:"absolute",top:2,right:2,width:3,height:3,background:C.green}}/>
        </div>
        <span style={{fontFamily:mono,fontSize:12,color:C.textPrimary,letterSpacing:"0.12em",fontWeight:700}}>POLICY ROOM</span>
      </div>
      <div style={{display:"flex",flex:1}}>
        {nav.map(item=>(<button key={item.id} onClick={()=>setView(item.id)} style={{background:"none",border:"none",cursor:"pointer",fontFamily:mono,fontSize:10,letterSpacing:"0.12em",color:view===item.id?C.green:C.textMuted,padding:"0 16px",height:52,borderBottom:view===item.id?`2px solid ${C.green}`:"2px solid transparent"}}>{item.label}</button>))}
      </div>
      <div style={{display:"flex",alignItems:"center",gap:6}}>
        <div style={{width:6,height:6,borderRadius:"50%",background:C.green,animation:"pulse 2s infinite"}}/>
        <span style={{fontFamily:mono,fontSize:10,color:C.textMuted,letterSpacing:"0.08em"}}>OPERATIONAL</span>
      </div>
    </div>
  );
}

function LandingPage({setView,setAnalysis}){
  const docTypes=["Legislation","Budget Papers","Regulatory Filings","Policy Memos","Research Reports"];
  const howItThinks=[
    {n:"01",title:"Stakeholder Analysis",sub:"Who wins, who loses, and who has the power to block.",body:"Every policy creates winners and losers. Policy Room maps the full stakeholder network and models influence, position, and alignment. The output is a visual graph, not a list of names."},
    {n:"02",title:"Political Risk Assessment",sub:"What can go wrong, and where the real exposure sits.",body:"Risk scores are broken into distinct categories so decision-makers know which dimension requires attention. Uncertainty is explicit: the tool flags what it does not know, not just what it does."},
    {n:"03",title:"Executive Briefing",sub:"One page. One minute. A clear recommended position.",body:"The executive brief is structured the way policy staff actually prepare ministerial documents: issue, context, political risk, media risk, recommended position. It exists to support a decision."},
  ];
  return(
    <div style={{minHeight:"100vh",background:C.bg,paddingTop:52}}>
      <div style={{position:"relative",overflow:"hidden",minHeight:"88vh",display:"flex",flexDirection:"column",alignItems:"center",justifyContent:"center",padding:"60px 32px 80px"}}>
        <div style={{position:"absolute",inset:0,backgroundImage:`linear-gradient(${C.border}44 1px,transparent 1px),linear-gradient(90deg,${C.border}44 1px,transparent 1px)`,backgroundSize:"48px 48px",maskImage:"radial-gradient(ellipse 80% 60% at 50% 40%,black,transparent)"}}/>
        <div style={{position:"absolute",top:"30%",left:"50%",transform:"translate(-50%,-50%)",width:600,height:300,background:C.green,opacity:0.03,borderRadius:"50%",filter:"blur(80px)"}}/>
        <div style={{position:"relative",width:"100%",maxWidth:1060}}>
          <div style={{textAlign:"center",marginBottom:44}}>
            <div style={{fontFamily:display,fontSize:"clamp(13px,1.5vw,17px)",color:C.green,letterSpacing:"0.04em",marginBottom:12,fontStyle:"italic"}}>Policy Intelligence Platform</div>
            <h1 style={{fontFamily:display,fontSize:"clamp(26px,4.2vw,50px)",color:C.textPrimary,fontWeight:400,lineHeight:1.1,margin:"0 0 8px",letterSpacing:"-0.02em"}}>Transform 300-page policy documents</h1>
            <h1 style={{fontFamily:display,fontSize:"clamp(26px,4.2vw,50px)",color:C.green,fontWeight:400,lineHeight:1.1,margin:"0 0 24px",letterSpacing:"-0.02em",fontStyle:"italic"}}>into decision-ready intelligence.</h1>
            <p style={{fontFamily:sans,fontSize:15,color:C.textSecondary,lineHeight:1.75,maxWidth:520,margin:"0 auto 20px"}}>Built for policy analysts, think tanks, and government teams. Stakeholder influence mapping, political risk scoring, and executive briefing notes in under 60 seconds.</p>
            <div style={{fontFamily:sans,fontSize:13,color:C.textMuted,marginBottom:32,display:"flex",alignItems:"center",justifyContent:"center",gap:10,flexWrap:"wrap",textAlign:"center"}}>
              <div style={{width:20,height:1,background:C.green+"50",flexShrink:0}}/>
              <span>The sample analysis is built from original PPE thesis and policy research by <span style={{color:C.textSecondary}}>Amirlin Munkhbat</span> at UBC.</span>
              <div style={{width:20,height:1,background:C.green+"50",flexShrink:0}}/>
            </div>
            <div style={{display:"flex",gap:12,justifyContent:"center",flexWrap:"wrap",marginBottom:44}}>
              <button onClick={()=>setView("upload")} style={{background:C.green,color:C.bg,border:"none",fontFamily:mono,fontSize:11,letterSpacing:"0.1em",padding:"13px 28px",cursor:"pointer",borderRadius:2,fontWeight:700}}>UPLOAD DOCUMENT</button>
              <button onClick={()=>{setAnalysis(SAMPLE);setView("dashboard");}} style={{background:"none",color:C.green,border:`1px solid ${C.green}`,fontFamily:mono,fontSize:11,letterSpacing:"0.1em",padding:"13px 28px",cursor:"pointer",borderRadius:2}}>VIEW SAMPLE ANALYSIS</button>
            </div>
          </div>
          <div style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:6,padding:"24px 28px",marginBottom:12}}>
            <div style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:20,flexWrap:"wrap",gap:10}}>
              <div>
                <div style={{fontFamily:mono,fontSize:9,color:C.green,letterSpacing:"0.15em",marginBottom:4}}>STAKEHOLDER INFLUENCE MAP</div>
                <div style={{fontFamily:sans,fontSize:12,color:C.textSecondary}}>Charitable Tax Incentive Reform · Canada Federal · Confidence 85%</div>
              </div>
              <div style={{display:"flex",gap:8}}><Tag label="TAX POLICY" color={C.blue} bg={C.blue+"18"}/><Tag label="RISK 38" color={C.green} bg={C.green+"18"}/><Tag label="THESIS RESEARCH" color={C.purple} bg={C.purple+"18"}/></div>
            </div>
            <InfluenceMap stakeholders={SAMPLE.stakeholders} links={SAMPLE.influenceLinks}/>
            <div style={{marginTop:16,paddingTop:16,borderTop:`1px solid ${C.border}`,display:"flex",justifyContent:"space-between",alignItems:"center",flexWrap:"wrap",gap:8}}>
              <div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.08em"}}>BASED ON ORIGINAL UBC ECONOMICS THESIS RESEARCH · AMIRLIN MUNKHBAT</div>
              <button onClick={()=>{setAnalysis(SAMPLE);setView("dashboard");}} style={{background:"none",border:`1px solid ${C.border}`,color:C.green,fontFamily:mono,fontSize:9,letterSpacing:"0.1em",padding:"6px 14px",cursor:"pointer",borderRadius:2}}>OPEN FULL ANALYSIS</button>
            </div>
          </div>

          {/* Preview row: Executive Brief + Political Risk */}
          <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:12}}>
            <div style={{background:C.surface,border:`1px solid ${C.border}`,borderRadius:4,padding:"18px 22px",cursor:"pointer"}} onClick={()=>{setAnalysis(SAMPLE);setView("dashboard");}}>
              <div style={{fontFamily:mono,fontSize:9,color:C.green,letterSpacing:"0.15em",marginBottom:12}}>EXECUTIVE BRIEF PREVIEW</div>
              <div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.1em",marginBottom:4}}>ISSUE</div>
              <div style={{fontFamily:sans,fontSize:13,color:C.textPrimary,marginBottom:14,lineHeight:1.4}}>Federal charitable tax credit reform. Structural overhaul of Canada's donor incentive system.</div>
              <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:8,marginBottom:14}}>
                <div style={{background:C.card,border:`1px solid ${C.border}`,borderLeft:`3px solid ${C.greenDim}`,padding:"10px 12px",borderRadius:"0 2px 2px 0"}}>
                  <div style={{fontFamily:mono,fontSize:8,color:C.textMuted,letterSpacing:"0.1em",marginBottom:3}}>POLITICAL RISK</div>
                  <div style={{fontFamily:display,fontSize:16,color:C.greenDim}}>MODERATE</div>
                </div>
                <div style={{background:C.card,border:`1px solid ${C.border}`,borderLeft:`3px solid ${C.green}`,padding:"10px 12px",borderRadius:"0 2px 2px 0"}}>
                  <div style={{fontFamily:mono,fontSize:8,color:C.textMuted,letterSpacing:"0.1em",marginBottom:3}}>MEDIA RISK</div>
                  <div style={{fontFamily:display,fontSize:16,color:C.green}}>LOW</div>
                </div>
              </div>
              <div style={{background:C.green+"15",border:`1px solid ${C.green}40`,borderRadius:3,padding:"10px 14px"}}>
                <div style={{fontFamily:mono,fontSize:8,color:C.textMuted,letterSpacing:"0.1em",marginBottom:3}}>RECOMMENDED POSITION</div>
                <div style={{fontFamily:display,fontSize:15,color:C.green}}>SUPPORT WITH AMENDMENTS</div>
              </div>
              <div style={{marginTop:12,fontFamily:mono,fontSize:9,color:C.green,letterSpacing:"0.08em"}}>VIEW FULL BRIEF →</div>
            </div>

            <div style={{background:C.surface,border:`1px solid ${C.border}`,borderRadius:4,padding:"18px 22px",cursor:"pointer"}} onClick={()=>{setAnalysis(SAMPLE);setView("dashboard");}}>
              <div style={{fontFamily:mono,fontSize:9,color:C.green,letterSpacing:"0.15em",marginBottom:12}}>POLITICAL RISK PREVIEW</div>
              {SAMPLE.risks.slice(0,4).map((r,i)=>(
                <div key={i} style={{marginBottom:14}}>
                  <div style={{display:"flex",justifyContent:"space-between",marginBottom:5,alignItems:"center"}}>
                    <span style={{fontFamily:sans,fontSize:12,color:C.textSecondary}}>{r.category}</span>
                    <Tag label={r.label} color={r.color} bg={r.color+"18"}/>
                  </div>
                  <RiskBar score={r.score} color={r.color}/>
                </div>
              ))}
              <div style={{marginTop:4,fontFamily:mono,fontSize:9,color:C.green,letterSpacing:"0.08em"}}>VIEW FULL ASSESSMENT →</div>
            </div>
          </div>
        </div>
        <div style={{position:"absolute",bottom:0,left:0,right:0,borderTop:`1px solid ${C.border}`,padding:"7px 0",overflow:"hidden"}}>
          <div style={{display:"flex",gap:64,fontFamily:mono,fontSize:10,color:C.textMuted,letterSpacing:"0.08em",animation:"ticker 30s linear infinite",whiteSpace:"nowrap"}}>
            {["Charitable Tax Reform · RISK 38","BC Energy Regulation · RISK 55","Federal Budget Analysis · RISK 61","Housing Strategy · RISK 67","Bill C-27 · RISK 72","Charitable Tax Reform · RISK 38","BC Energy Regulation · RISK 55","Federal Budget Analysis · RISK 61"].map((t,i)=>(<span key={i}><span style={{color:C.green}}>◈</span> {t}</span>))}
          </div>
        </div>
      </div>

      <div style={{maxWidth:1060,margin:"0 auto",padding:"56px 32px 48px"}}>
        <SL>FLAGSHIP ANALYSIS</SL>
        <div onClick={()=>{setAnalysis(SAMPLE);setView("dashboard");}} style={{background:C.surface,border:`1px solid ${C.green}40`,borderRadius:4,padding:"24px 28px",cursor:"pointer",position:"relative",marginBottom:28}}>
          <div style={{position:"absolute",top:0,left:0,right:0,height:2,background:C.green,borderRadius:"4px 4px 0 0"}}/>
          <div style={{display:"flex",justifyContent:"space-between",alignItems:"flex-start",flexWrap:"wrap",gap:12,marginBottom:12}}>
            <div>
              <div style={{fontFamily:mono,fontSize:9,color:C.green,letterSpacing:"0.15em",marginBottom:6}}>ORIGINAL THESIS RESEARCH · UBC ECONOMICS · AMIRLIN MUNKHBAT</div>
              <div style={{fontFamily:display,fontSize:20,color:C.textPrimary,fontWeight:400,marginBottom:4,lineHeight:1.2}}>Canadian Charitable Tax Incentive Reform</div>
              <div style={{fontFamily:mono,fontSize:10,color:C.textMuted}}>Policy Research Brief · Canada · Federal</div>
            </div>
            <div style={{display:"flex",gap:10,alignItems:"center",flexWrap:"wrap"}}>
              <Tag label="TAX POLICY" color={C.blue} bg={C.blue+"18"}/>
              <Tag label="THESIS RESEARCH" color={C.purple} bg={C.purple+"18"}/>
              <div style={{textAlign:"right"}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted}}>RISK</div><div style={{fontFamily:display,fontSize:26,color:C.green,lineHeight:1}}>38</div></div>
              <div style={{textAlign:"right"}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted}}>CONFIDENCE</div><div style={{fontFamily:display,fontSize:26,color:C.green,lineHeight:1}}>85%</div></div>
            </div>
          </div>
          <p style={{fontFamily:sans,fontSize:13,color:C.textSecondary,lineHeight:1.7,margin:"0 0 12px",maxWidth:680}}>Analysis of Canada's charitable tax credit system, structurally unchanged since 1988, drawing on original economic modelling, Rawlsian justice theory, and Department of Finance elasticity data. Argues the current regime is regressive by design and models three reform options with distinct feasibility profiles.</p>
          <div style={{display:"flex",justifyContent:"space-between",alignItems:"center"}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted}}>Includes: Stakeholder Influence Map · Executive Brief · Political Landscape · Reform Option Modelling</div><span style={{fontFamily:mono,fontSize:10,color:C.green}}>OPEN FULL ANALYSIS</span></div>
        </div>
        <div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.1em",marginBottom:10}}>OTHER DOCUMENT TYPES SUPPORTED</div>
        <div style={{display:"grid",gridTemplateColumns:"repeat(auto-fit,minmax(200px,1fr))",gap:8}}>
          {DEMOS.map((demo,i)=>(<div key={i} onClick={()=>{setAnalysis(SAMPLE);setView("dashboard");}} style={{background:C.card,border:`1px solid ${C.border}`,padding:"14px 16px",cursor:"pointer",borderRadius:3,display:"flex",justifyContent:"space-between",alignItems:"center",gap:10}}><div><div style={{fontFamily:sans,fontSize:12,color:C.textPrimary,fontWeight:500,marginBottom:2}}>{demo.label}</div><div style={{fontFamily:mono,fontSize:9,color:C.textMuted}}>{demo.type}</div></div><Tag label={demo.tag} color={C.blue} bg={C.blue+"18"}/></div>))}
        </div>
      </div>

      <div style={{background:C.surface,borderTop:`1px solid ${C.border}`}}>
        <div style={{maxWidth:1060,margin:"0 auto",padding:"48px 32px"}}>
          <SL>HOW IT THINKS</SL>
          <p style={{fontFamily:sans,fontSize:14,color:C.textMuted,marginBottom:28,maxWidth:520,lineHeight:1.7}}>Policy Room does not summarize documents. It applies the same analytical framework a senior analyst would, working through stakeholders, risk, and political context before surfacing recommendations.</p>
          <div style={{display:"grid",gridTemplateColumns:"repeat(auto-fit,minmax(260px,1fr))",gap:2}}>
            {howItThinks.map(h=>(<div key={h.n} style={{background:C.card,border:`1px solid ${C.border}`,padding:"24px 24px"}}><div style={{fontFamily:mono,fontSize:10,color:C.green,letterSpacing:"0.12em",marginBottom:14}}>{h.n} · {h.title.toUpperCase()}</div><div style={{fontFamily:display,fontSize:16,color:C.textPrimary,marginBottom:10,lineHeight:1.3}}>{h.sub}</div><p style={{fontFamily:sans,fontSize:13,color:C.textSecondary,lineHeight:1.7,margin:0}}>{h.body}</p></div>))}
          </div>
        </div>
      </div>

      <div style={{borderTop:`1px solid ${C.border}`,borderBottom:`1px solid ${C.border}`,background:C.surface}}>
        <div style={{maxWidth:1060,margin:"0 auto",padding:"18px 32px",display:"flex",alignItems:"center",gap:18,flexWrap:"wrap"}}>
          <span style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.12em",whiteSpace:"nowrap"}}>ACCEPTS</span>
          {docTypes.map(t=><Tag key={t} label={t} color={C.textSecondary}/>)}
        </div>
      </div>
      <div style={{padding:"18px 32px",display:"flex",justifyContent:"space-between",flexWrap:"wrap",gap:10}}>
        <p style={{fontFamily:mono,fontSize:10,color:C.textMuted,margin:0}}>POLICY ROOM · DECISION SUPPORT TOOL</p>
        <p style={{fontFamily:mono,fontSize:10,color:C.textMuted,margin:0}}>Built by <span style={{color:C.textSecondary}}>Amirlin Munkhbat</span></p>
      </div>
      <style>{`@keyframes ticker{from{transform:translateX(0)}to{transform:translateX(-50%)}}@keyframes pulse{0%,100%{opacity:1}50%{opacity:0.3}}`}</style>
    </div>
  );
}

function UploadRoom({setView,setAnalysis}){
  const [dragOver,setDragOver]=useState(false);
  const [file,setFile]=useState(null);
  const [stage,setStage]=useState(0); // 0=idle 1=uploaded 2=analyzing 3=done
  const [processing,setProcessing]=useState(false);
  const inputRef=useRef();
  const handleFile=(f)=>{if(!f)return;setFile(f);setStage(1);};
  const runAnalysis=async()=>{
    if(!file)return;
    setProcessing(true);setStage(2);
    try{
      const sys=`You are Policy Room, a government intelligence analysis platform. Respond ONLY with valid JSON. No preamble, no markdown fences. Return: {"meta":{"title":"...","type":"...","jurisdiction":"...","date":"YYYY-MM-DD","pages":0,"wordCount":"...","classification":"PUBLIC","analyst":"Policy Room Intelligence","riskScore":0,"completeness":0,"confidence":0,"dataCoverage":"High|Medium|Low","missingInfo":["..."]},"executive":"2-4 sentences","issues":[{"id":1,"title":"...","severity":"critical|high|medium|low","tags":["..."],"summary":"..."}],"stakeholders":[{"name":"...","role":"...","influence":0,"position":"supportive|opposed|mixed","notes":"...","group":"government|industry|ngo|regulator|citizens"}],"influenceLinks":[{"source":"...","target":"...","strength":0.0,"type":"align|conflict"}],"winnersLosers":{"winners":[{"actor":"...","reason":"..."}],"losers":[{"actor":"...","reason":"..."}]},"risks":[{"category":"...","score":0,"label":"HIGH|ELEVATED|MODERATE|LOW","detail":"...","color":"#e05252"}],"economic":{"gdpImpact":"...","complianceCost":"...","sectorImpact":[{"sector":"...","impact":"positive|negative|neutral","magnitude":0}]},"ministerBrief":{"issue":"...","whatHappened":"para1\\n\\npara2","politicalRisk":"HIGH|ELEVATED|MODERATE|LOW","politicalRiskDetail":"...","mediaRisk":"HIGH|ELEVATED|MODERATE|LOW","mediaRiskDetail":"...","recommendedPosition":"SUPPORT|SUPPORT WITH AMENDMENTS|OPPOSE|MONITOR","recommendedPositionDetail":"..."},"mediaNarrative":{"industryReaction":"...","oppositionReaction":"...","probableHeadline":"...","secondaryHeadline":"...","emergingCoalition":"...","narrativeRisk":"..."},"recommendations":[{"priority":"IMMEDIATE|SHORT-TERM|MEDIUM-TERM|ONGOING","action":"..."}],"jurisdictions":[{"name":"...","framework":"...","alignment":0,"notes":"..."}]}`;
      const resp=await fetch("https://api.anthropic.com/v1/messages",{method:"POST",headers:{"Content-Type":"application/json"},body:JSON.stringify({model:"claude-sonnet-4-20250514",max_tokens:4000,system:sys,messages:[{role:"user",content:`Filename: ${file.name}\nSize: ${(file.size/1024).toFixed(1)} KB`}]})});
      const data=await resp.json();
      const raw=data.content?.[0]?.text||"";
      let parsed;
      try{parsed=JSON.parse(raw.replace(/```json|```/g,"").trim());}
      catch{parsed=SAMPLE;}
      setStage(3);setAnalysis(parsed);setTimeout(()=>setView("dashboard"),900);
    }catch(err){setStage(3);setAnalysis(SAMPLE);setTimeout(()=>setView("dashboard"),900);}
    setProcessing(false);
  };
  const stages=[
    {n:1,label:"Document uploaded"},
    {n:2,label:"Analysis running"},
    {n:3,label:"Brief ready"},
  ];
  return(
    <div style={{minHeight:"100vh",background:C.bg,paddingTop:52,display:"flex",alignItems:"center",justifyContent:"center",padding:"80px 32px"}}>
      <div style={{width:"100%",maxWidth:620}}>
        <div style={{marginBottom:28}}>
          <div style={{fontFamily:mono,fontSize:10,color:C.green,letterSpacing:"0.15em",marginBottom:10}}>DOCUMENT INTAKE</div>
          <h2 style={{fontFamily:display,fontSize:32,color:C.textPrimary,fontWeight:400,margin:"0 0 8px"}}>Upload Policy Document</h2>
          <p style={{fontFamily:sans,fontSize:14,color:C.textSecondary}}>Accepts: Legislation, Budget Papers, Regulatory Filings, Memos, Research Reports</p>
        </div>
        <div onDragOver={e=>{e.preventDefault();setDragOver(true);}} onDragLeave={()=>setDragOver(false)} onDrop={e=>{e.preventDefault();setDragOver(false);handleFile(e.dataTransfer.files[0]);}} onClick={()=>!file&&inputRef.current.click()} style={{border:`2px dashed ${dragOver?C.green:file?C.greenDim:C.border}`,borderRadius:4,padding:"44px 28px",textAlign:"center",cursor:file?"default":"pointer",background:dragOver?C.greenFaint:C.surface,marginBottom:20}}>
          <input ref={inputRef} type="file" accept=".pdf" style={{display:"none"}} onChange={e=>handleFile(e.target.files[0])}/>
          {file?(<div><div style={{fontFamily:mono,fontSize:22,color:C.green,marginBottom:10}}>◈</div><div style={{fontFamily:sans,fontSize:14,color:C.textPrimary,fontWeight:600}}>{file.name}</div><div style={{fontFamily:mono,fontSize:11,color:C.textMuted,marginTop:4}}>{(file.size/1024).toFixed(1)} KB</div><button onClick={e=>{e.stopPropagation();setFile(null);setStage(0);}} style={{marginTop:14,background:"none",border:`1px solid ${C.border}`,color:C.textMuted,fontFamily:mono,fontSize:10,cursor:"pointer",padding:"5px 14px",borderRadius:2}}>REMOVE</button></div>):(<div><div style={{fontSize:36,color:C.textMuted,marginBottom:10}}>⬆</div><div style={{fontFamily:sans,fontSize:14,color:C.textSecondary}}>Drop PDF here or click to browse</div><div style={{fontFamily:mono,fontSize:10,color:C.textMuted,marginTop:6,letterSpacing:"0.08em"}}>MAX 50MB · PDF FORMAT</div></div>)}
        </div>
        <div style={{textAlign:"center",marginBottom:20}}><button onClick={()=>{setAnalysis(SAMPLE);setView("dashboard");}} style={{background:"none",border:"none",color:C.textMuted,fontFamily:mono,fontSize:10,cursor:"pointer",textDecoration:"underline"}}>or load sample analysis (Charitable Tax Reform)</button></div>

        {/* Analyst-focused progress — only shown when processing */}
        {stage>=2&&(
          <div style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"16px 20px",marginBottom:20}}>
            <div style={{display:"flex",gap:0}}>
              {stages.map((s,i)=>{
                const done=stage>s.n;
                const active=stage===s.n;
                const col=done||active?C.green:C.textMuted;
                return(
                  <div key={s.n} style={{flex:1,display:"flex",flexDirection:"column",alignItems:"center",gap:6}}>
                    <div style={{display:"flex",alignItems:"center",width:"100%"}}>
                      {i>0&&<div style={{flex:1,height:2,background:done?C.green:C.border}}/>}
                      <div style={{width:20,height:20,borderRadius:"50%",background:done?"none":active?C.green+"30":"none",border:`2px solid ${col}`,display:"flex",alignItems:"center",justifyContent:"center",flexShrink:0}}>
                        {done?<span style={{color:C.green,fontSize:10,lineHeight:1}}>✓</span>:<div style={{width:6,height:6,borderRadius:"50%",background:active?C.green:C.border}}/>}
                      </div>
                      {i<stages.length-1&&<div style={{flex:1,height:2,background:done?C.green:C.border}}/>}
                    </div>
                    <div style={{fontFamily:mono,fontSize:9,color:col,letterSpacing:"0.06em",textAlign:"center"}}>{s.label}</div>
                  </div>
                );
              })}
            </div>
          </div>
        )}

        <button disabled={!file||processing} onClick={runAnalysis} style={{width:"100%",padding:"15px",borderRadius:2,border:"none",cursor:file&&!processing?"pointer":"not-allowed",background:file&&!processing?C.green:C.surface,color:file&&!processing?C.bg:C.textMuted,fontFamily:mono,fontSize:12,letterSpacing:"0.1em",fontWeight:700}}>
          {processing?"GENERATING BRIEF...":"GENERATE INTELLIGENCE BRIEF"}
        </button>
      </div>
    </div>
  );
}

function Dashboard({data,setView}){
  const d=data||SAMPLE;
  const [tab,setTab]=useState("assessment");
  const pc=(p)=>p==="supportive"?C.green:p==="opposed"?C.red:C.amber;
  const tabs=[{id:"assessment",label:"INTELLIGENCE ASSESSMENT"},{id:"executive",label:"EXECUTIVE BRIEF",badge:true},{id:"political",label:"POLITICAL LANDSCAPE",badge:true}];
  const mb=d.ministerBrief||{issue:d.meta.title,whatHappened:d.executive,politicalRisk:"ELEVATED",politicalRiskDetail:"See full analysis.",mediaRisk:"MODERATE",mediaRiskDetail:"Monitor coverage.",recommendedPosition:"UNDER REVIEW",recommendedPositionDetail:"Consult full brief."};
  const mn=d.mediaNarrative||{industryReaction:"Upload a document.",oppositionReaction:"Upload a document.",probableHeadline:"",secondaryHeadline:"",emergingCoalition:"Upload a document.",narrativeRisk:"Upload a document."};
  const rc=(r)=>r==="HIGH"?C.red:r==="ELEVATED"?C.amber:r==="LOW"?C.green:C.greenDim;
  const posc=(p)=>p.includes("SUPPORT")?C.green:p.includes("OPPOSE")?C.red:C.amber;
  return(
    <div style={{minHeight:"100vh",background:C.bg,paddingTop:52}}>
      <div style={{borderBottom:`1px solid ${C.border}`,background:C.surface,padding:"20px 32px"}}>
        <div style={{maxWidth:1160,margin:"0 auto"}}>
          <div style={{display:"flex",justifyContent:"space-between",alignItems:"flex-start",flexWrap:"wrap",gap:14}}>
            <div>
              <div style={{fontFamily:mono,fontSize:10,color:C.green,letterSpacing:"0.15em",marginBottom:6}}>INTELLIGENCE BRIEF · {d.meta.classification}</div>
              <h2 style={{fontFamily:display,fontSize:"clamp(14px,2.2vw,22px)",color:C.textPrimary,fontWeight:400,margin:"0 0 10px",maxWidth:640}}>{d.meta.title}</h2>
              <div style={{display:"flex",gap:8,flexWrap:"wrap"}}><Tag label={d.meta.type} color={C.blue} bg={C.blue+"18"}/><Tag label={d.meta.jurisdiction}/><Tag label={`${d.meta.pages} PAGES`}/><Tag label={d.meta.date}/>{d.meta.researchBacked&&<Tag label="THESIS RESEARCH" color={C.purple} bg={C.purple+"18"}/>}</div>
            </div>
            <div style={{display:"flex",flexDirection:"column",alignItems:"flex-end",gap:8}}>
              <div style={{display:"flex",gap:10}}>
                <div style={{background:C.card,border:`1px solid ${C.border}`,padding:"9px 16px",borderRadius:4,textAlign:"center"}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.1em",marginBottom:2}}>RISK</div><div style={{fontFamily:display,fontSize:30,lineHeight:1,color:d.meta.riskScore>=70?C.red:d.meta.riskScore>=50?C.amber:C.green}}>{d.meta.riskScore}</div></div>
                <div style={{background:C.card,border:`1px solid ${C.border}`,padding:"9px 16px",borderRadius:4,textAlign:"center"}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.1em",marginBottom:2}}>CONFIDENCE</div><div style={{fontFamily:display,fontSize:30,lineHeight:1,color:(d.meta.confidence||85)>=80?C.green:C.amber}}>{d.meta.confidence||85}%</div></div>
              </div>
              <button onClick={()=>setView("brief")} style={{background:C.green,color:C.bg,border:"none",fontFamily:mono,fontSize:10,letterSpacing:"0.1em",padding:"8px 16px",cursor:"pointer",borderRadius:2,fontWeight:700}}>GENERATE BRIEFING</button>
            </div>
          </div>
        </div>
      </div>
      <div style={{borderBottom:`1px solid ${C.border}`,background:C.surface,padding:"0 32px"}}>
        <div style={{maxWidth:1160,margin:"0 auto",display:"flex"}}>
          {tabs.map(t=>(<button key={t.id} onClick={()=>setTab(t.id)} style={{background:"none",border:"none",cursor:"pointer",fontFamily:mono,fontSize:10,letterSpacing:"0.1em",color:tab===t.id?C.green:C.textMuted,padding:"13px 20px",borderBottom:tab===t.id?`2px solid ${C.green}`:"2px solid transparent",whiteSpace:"nowrap",display:"flex",alignItems:"center",gap:6}}>{t.label}{t.badge&&<span style={{background:C.green+"20",color:C.green,fontSize:8,padding:"1px 5px",borderRadius:2}}>NEW</span>}</button>))}
        </div>
      </div>
      <div style={{maxWidth:1160,margin:"0 auto",padding:"28px 32px"}}>
        {tab==="assessment"&&(
          <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:18}}>
            <div style={{gridColumn:"1 / -1",background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>EXECUTIVE SUMMARY</SL>
              <p style={{fontFamily:sans,fontSize:14,color:C.textSecondary,lineHeight:1.8,margin:0}}>{d.executive}</p>
            </div>
            <div style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>ANALYTICAL CONFIDENCE</SL>
              <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:16,marginBottom:16}}>
                <div><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.12em",marginBottom:6}}>CONFIDENCE SCORE</div><div style={{fontFamily:display,fontSize:36,color:(d.meta.confidence||85)>=80?C.green:C.amber,lineHeight:1,marginBottom:6}}>{d.meta.confidence||85}%</div><RiskBar score={d.meta.confidence||85} color={(d.meta.confidence||85)>=80?C.green:C.amber}/></div>
                <div><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.12em",marginBottom:6}}>DATA COVERAGE</div><div style={{fontFamily:sans,fontSize:14,color:C.textPrimary,marginBottom:4}}>{d.meta.dataCoverage||"High"}</div></div>
              </div>
              {d.meta.missingInfo?.length>0&&(<div style={{background:"#f5a62310",border:"1px solid #f5a62330",borderRadius:3,padding:"12px 14px"}}><div style={{fontFamily:mono,fontSize:9,color:C.amber,letterSpacing:"0.12em",marginBottom:6}}>DATA GAPS</div>{d.meta.missingInfo.map((item,i)=>(<div key={i} style={{display:"flex",gap:8,marginBottom:3}}><span style={{color:C.amber,fontFamily:mono,fontSize:10}}>-</span><span style={{fontFamily:sans,fontSize:12,color:C.textSecondary,lineHeight:1.5}}>{item}</span></div>))}</div>)}
            </div>
            <div style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>KEY POLICY ISSUES</SL>
              <div style={{display:"flex",flexDirection:"column",gap:10}}>
                {d.issues.map(issue=>(<div key={issue.id} style={{border:`1px solid ${C.border}`,borderRadius:3,padding:"11px 14px",background:C.surface}}><div style={{display:"flex",alignItems:"center",gap:8,marginBottom:5,flexWrap:"wrap"}}><span style={{fontFamily:mono,fontSize:10,color:C.textMuted}}>#{String(issue.id).padStart(2,"0")}</span><span style={{fontFamily:sans,fontSize:13,fontWeight:600,color:C.textPrimary}}>{issue.title}</span><SB level={issue.severity}/>{issue.tags.map(t=><Tag key={t} label={t}/>)}</div><p style={{fontFamily:sans,fontSize:12,color:C.textSecondary,margin:0,lineHeight:1.6}}>{issue.summary}</p></div>))}
              </div>
            </div>
            <div style={{gridColumn:"1 / -1",background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>STAKEHOLDER INFLUENCE MAP</SL>
              <p style={{fontFamily:sans,fontSize:12,color:C.textMuted,marginBottom:18}}>Stakeholder network showing influence levels, political position, and alignment/conflict relationships.</p>
              <InfluenceMap stakeholders={d.stakeholders} links={d.influenceLinks||SAMPLE.influenceLinks}/>
            </div>
            <div style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>STAKEHOLDER DETAIL</SL>
              {d.stakeholders.map((s,i)=>(<div key={i} style={{paddingBottom:10,marginBottom:10,borderBottom:i<d.stakeholders.length-1?`1px solid ${C.border}`:"none"}}><div style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:5}}><div><div style={{fontFamily:sans,fontSize:13,fontWeight:600,color:C.textPrimary}}>{s.name}</div><div style={{fontFamily:mono,fontSize:10,color:C.textMuted}}>{s.role}</div></div><Tag label={s.position.toUpperCase()} color={pc(s.position)} bg={pc(s.position)+"18"}/></div><div style={{marginBottom:4}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,marginBottom:2}}>INFLUENCE {s.influence}/100</div><RiskBar score={s.influence} color={pc(s.position)}/></div><div style={{fontFamily:sans,fontSize:12,color:C.textMuted,lineHeight:1.5}}>{s.notes}</div></div>))}
            </div>
            <div style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>WINNERS AND LOSERS</SL>
              <div style={{marginBottom:18}}><div style={{fontFamily:mono,fontSize:10,color:C.green,letterSpacing:"0.1em",marginBottom:10}}>WINNERS</div>{d.winnersLosers.winners.map((w,i)=>(<div key={i} style={{marginBottom:10,paddingLeft:12,borderLeft:`2px solid ${C.green}`}}><div style={{fontFamily:sans,fontSize:13,fontWeight:600,color:C.textPrimary}}>{w.actor}</div><div style={{fontFamily:sans,fontSize:12,color:C.textSecondary,marginTop:2}}>{w.reason}</div></div>))}</div>
              <div><div style={{fontFamily:mono,fontSize:10,color:C.red,letterSpacing:"0.1em",marginBottom:10}}>LOSERS</div>{d.winnersLosers.losers.map((w,i)=>(<div key={i} style={{marginBottom:10,paddingLeft:12,borderLeft:`2px solid ${C.red}`}}><div style={{fontFamily:sans,fontSize:13,fontWeight:600,color:C.textPrimary}}>{w.actor}</div><div style={{fontFamily:sans,fontSize:12,color:C.textSecondary,marginTop:2}}>{w.reason}</div></div>))}</div>
            </div>
            <div style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>RISK ASSESSMENT</SL>
              {d.risks.map((r,i)=>(<div key={i} style={{marginBottom:16}}><div style={{display:"flex",justifyContent:"space-between",marginBottom:5,alignItems:"center"}}><span style={{fontFamily:sans,fontSize:13,fontWeight:600,color:C.textPrimary}}>{r.category}</span><Tag label={r.label} color={r.color} bg={r.color+"18"}/></div><RiskBar score={r.score} color={r.color}/><div style={{fontFamily:sans,fontSize:12,color:C.textMuted,marginTop:5,lineHeight:1.5}}>{r.detail}</div></div>))}
            </div>
            <div style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>ECONOMIC IMPACT</SL>
              <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:14,marginBottom:18}}>
                <div style={{background:C.surface,border:`1px solid ${C.border}`,padding:"12px",borderRadius:3}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.1em",marginBottom:4}}>GDP IMPACT</div><div style={{fontFamily:display,fontSize:16,color:C.textPrimary}}>{d.economic.gdpImpact}</div></div>
                <div style={{background:C.surface,border:`1px solid ${C.border}`,padding:"12px",borderRadius:3}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.1em",marginBottom:4}}>FISCAL COST</div><div style={{fontFamily:display,fontSize:14,color:C.textPrimary}}>{d.economic.complianceCost}</div></div>
              </div>
              {d.economic.sectorImpact.map((s,i)=>(<div key={i} style={{display:"flex",alignItems:"center",gap:10,marginBottom:7}}><span style={{fontFamily:sans,fontSize:12,color:C.textSecondary,minWidth:130}}>{s.sector}</span><div style={{display:"flex",gap:3}}>{[1,2,3,4,5].map(n=><div key={n} style={{width:10,height:10,borderRadius:1,background:n<=s.magnitude?(s.impact==="positive"?C.green:s.impact==="negative"?C.red:C.amber):C.border}}/>)}</div><Tag label={s.impact.toUpperCase()} color={s.impact==="positive"?C.green:s.impact==="negative"?C.red:C.amber}/></div>))}
            </div>
            <div style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>JURISDICTIONAL COMPARISON</SL>
              {d.jurisdictions.map((j,i)=>(<div key={i} style={{marginBottom:14,paddingBottom:14,borderBottom:i<d.jurisdictions.length-1?`1px solid ${C.border}`:"none"}}><div style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:4}}><div><span style={{fontFamily:sans,fontSize:13,fontWeight:600,color:C.textPrimary}}>{j.name}</span><span style={{fontFamily:mono,fontSize:10,color:C.textMuted,marginLeft:8}}>{j.framework}</span></div><span style={{fontFamily:mono,fontSize:12,color:j.alignment>=70?C.green:j.alignment>=50?C.amber:C.red}}>{j.alignment}%</span></div><RiskBar score={j.alignment} color={j.alignment>=70?C.green:j.alignment>=50?C.amber:C.red}/><div style={{fontFamily:sans,fontSize:12,color:C.textMuted,marginTop:5}}>{j.notes}</div></div>))}
            </div>
            <div style={{gridColumn:"1 / -1",background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>RECOMMENDATIONS</SL>
              <div style={{display:"grid",gridTemplateColumns:"repeat(auto-fit,minmax(280px,1fr))",gap:10}}>
                {d.recommendations.map((r,i)=>{const pColor=r.priority==="IMMEDIATE"?C.red:r.priority==="SHORT-TERM"?C.amber:r.priority==="MEDIUM-TERM"?C.blue:C.textMuted;return(<div key={i} style={{background:C.surface,border:`1px solid ${C.border}`,borderLeft:`3px solid ${pColor}`,padding:"14px 18px",borderRadius:"0 3px 3px 0"}}><Tag label={r.priority} color={pColor} bg={pColor+"18"}/><p style={{fontFamily:sans,fontSize:13,color:C.textSecondary,margin:"8px 0 0",lineHeight:1.6}}>{r.action}</p></div>);})}
              </div>
            </div>
          </div>
        )}
        {tab==="executive"&&(
          <div style={{maxWidth:720,margin:"0 auto"}}>
            <div style={{borderTop:`3px solid ${C.green}`,borderBottom:`1px solid ${C.border}`,padding:"18px 0 14px",marginBottom:24}}>
              <div style={{fontFamily:mono,fontSize:9,color:C.green,letterSpacing:"0.15em",marginBottom:6}}>EXECUTIVE BRIEF · ONE MINUTE READ</div>
              <div style={{fontFamily:display,fontSize:20,color:C.textPrimary,fontWeight:400,marginBottom:4}}>{d.meta.title}</div>
              <div style={{display:"flex",gap:8,flexWrap:"wrap"}}><Tag label={d.meta.type} color={C.blue} bg={C.blue+"18"}/><Tag label={d.meta.jurisdiction}/></div>
            </div>
            <div style={{marginBottom:20}}><div style={{fontFamily:mono,fontSize:9,color:C.green,letterSpacing:"0.15em",marginBottom:8}}>ISSUE</div><div style={{fontFamily:sans,fontSize:15,color:C.textPrimary,lineHeight:1.5,fontWeight:500}}>{mb.issue}</div></div>
            <div style={{marginBottom:20}}><div style={{fontFamily:mono,fontSize:9,color:C.green,letterSpacing:"0.15em",marginBottom:8}}>WHAT HAPPENED</div><div style={{background:C.surface,border:`1px solid ${C.border}`,borderLeft:`3px solid ${C.green}`,padding:"16px 18px",borderRadius:"0 3px 3px 0"}}>{mb.whatHappened.split("\n\n").map((para,i)=>(<p key={i} style={{fontFamily:sans,fontSize:13,color:C.textSecondary,lineHeight:1.8,margin:i>0?"10px 0 0":0}}>{para}</p>))}</div></div>
            <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:14,marginBottom:20}}>
              <div style={{background:C.surface,border:`1px solid ${C.border}`,borderLeft:`3px solid ${rc(mb.politicalRisk)}`,padding:"14px 18px",borderRadius:"0 3px 3px 0"}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.12em",marginBottom:4}}>POLITICAL RISK</div><div style={{fontFamily:display,fontSize:20,color:rc(mb.politicalRisk),marginBottom:6}}>{mb.politicalRisk}</div><div style={{fontFamily:sans,fontSize:12,color:C.textSecondary,lineHeight:1.6}}>{mb.politicalRiskDetail}</div></div>
              <div style={{background:C.surface,border:`1px solid ${C.border}`,borderLeft:`3px solid ${rc(mb.mediaRisk)}`,padding:"14px 18px",borderRadius:"0 3px 3px 0"}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.12em",marginBottom:4}}>MEDIA RISK</div><div style={{fontFamily:display,fontSize:20,color:rc(mb.mediaRisk),marginBottom:6}}>{mb.mediaRisk}</div><div style={{fontFamily:sans,fontSize:12,color:C.textSecondary,lineHeight:1.6}}>{mb.mediaRiskDetail}</div></div>
            </div>
            <div style={{background:posc(mb.recommendedPosition)+"15",border:`1px solid ${posc(mb.recommendedPosition)}40`,borderRadius:4,padding:"18px 22px"}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.12em",marginBottom:4}}>RECOMMENDED POSITION</div><div style={{fontFamily:display,fontSize:22,color:posc(mb.recommendedPosition),marginBottom:8}}>{mb.recommendedPosition}</div><div style={{fontFamily:sans,fontSize:13,color:C.textSecondary,lineHeight:1.7}}>{mb.recommendedPositionDetail}</div></div>
          </div>
        )}
        {tab==="political"&&(
          <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:18}}>
            <div style={{gridColumn:"1 / -1",background:C.surface,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}>
              <SL>PROJECTED MEDIA COVERAGE</SL>
              <div style={{marginBottom:16}}><div style={{fontFamily:mono,fontSize:9,color:C.green,letterSpacing:"0.1em",marginBottom:8}}>PRIMARY HEADLINE</div><div style={{fontFamily:display,fontSize:18,color:C.textPrimary,lineHeight:1.4,borderLeft:`3px solid ${C.green}`,paddingLeft:14}}>{mn.probableHeadline}</div></div>
              {mn.secondaryHeadline&&(<div><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.1em",marginBottom:8}}>SECONDARY HEADLINE · OPPOSITION FRAMING</div><div style={{fontFamily:display,fontSize:15,color:C.textSecondary,lineHeight:1.4,borderLeft:`3px solid ${C.red}`,paddingLeft:14}}>{mn.secondaryHeadline}</div></div>)}
            </div>
            {[[mn.industryReaction,"INDUSTRY REACTION"],[mn.oppositionReaction,"OPPOSITION REACTION"],[mn.emergingCoalition,"EMERGING COALITION"],[mn.narrativeRisk,"NARRATIVE RISK"]].map(([text,label],i)=>(<div key={i} style={{background:C.card,border:`1px solid ${C.border}`,borderRadius:4,padding:"20px 24px"}}><SL>{label}</SL><p style={{fontFamily:sans,fontSize:13,color:C.textSecondary,lineHeight:1.75,margin:0}}>{text}</p></div>))}
          </div>
        )}
      </div>
      <div style={{borderTop:`1px solid ${C.border}`,padding:"12px 32px",display:"flex",justifyContent:"space-between"}}><span style={{fontFamily:mono,fontSize:9,color:C.textMuted}}>POLICY ROOM · DECISION SUPPORT TOOL</span><span style={{fontFamily:mono,fontSize:9,color:C.textMuted}}>Built by <span style={{color:C.textSecondary}}>Amirlin Munkhbat</span></span></div>
    </div>
  );
}

function BriefingNote({data}){
  const d=data||SAMPLE;
  const today=new Date().toLocaleDateString("en-CA",{year:"numeric",month:"long",day:"numeric"});
  const conf=d.meta.confidence||85;
  const confColor=conf>=80?C.green:conf>=60?C.amber:C.red;
  return(
    <div style={{minHeight:"100vh",background:C.bg,paddingTop:52}}>
      <div style={{maxWidth:780,margin:"0 auto",padding:"36px"}}>
        <div style={{borderTop:`3px solid ${C.green}`,borderBottom:`1px solid ${C.border}`,padding:"20px 0 16px",marginBottom:24}}>
          <div style={{display:"flex",justifyContent:"space-between",alignItems:"flex-start",flexWrap:"wrap",gap:10}}>
            <div><div style={{fontFamily:mono,fontSize:10,color:C.green,letterSpacing:"0.15em",marginBottom:4}}>POLICY ROOM · INTELLIGENCE BRIEFING NOTE</div><h1 style={{fontFamily:display,fontSize:24,color:C.textPrimary,fontWeight:400,margin:"0 0 4px"}}>POLICY ANALYSIS BRIEF</h1><div style={{fontFamily:mono,fontSize:10,color:C.textMuted}}>{d.meta.title}</div></div>
            <div style={{textAlign:"right"}}><div style={{fontFamily:mono,fontSize:10,color:C.textMuted,marginBottom:2}}>DATE PREPARED</div><div style={{fontFamily:mono,fontSize:11,color:C.textPrimary}}>{today}</div><div style={{marginTop:6}}><Tag label={d.meta.classification} color={C.green} bg="#00e5a015"/></div></div>
          </div>
          <div style={{display:"flex",gap:18,marginTop:14,paddingTop:14,borderTop:`1px solid ${C.border}`,flexWrap:"wrap"}}>
            {[["TYPE",d.meta.type,null],["JURISDICTION",d.meta.jurisdiction,null],["RISK",`${d.meta.riskScore}/100`,d.meta.riskScore>=70?C.red:C.amber],["CONFIDENCE",`${conf}%`,confColor]].map(([k,v,c])=>(<div key={k}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.1em"}}>{k}</div><div style={{fontFamily:mono,fontSize:11,color:c||C.textPrimary,marginTop:1}}>{v}</div></div>))}
          </div>
        </div>
        {d.meta.missingInfo?.length>0&&(<div style={{background:"#f5a62310",border:"1px solid #f5a62330",borderRadius:3,padding:"12px 18px",marginBottom:20}}><div style={{fontFamily:mono,fontSize:9,color:C.amber,letterSpacing:"0.12em",marginBottom:6}}>DATA GAPS</div>{d.meta.missingInfo.map((item,i)=>(<div key={i} style={{fontFamily:sans,fontSize:12,color:C.textSecondary,marginBottom:2}}>- {item}</div>))}</div>)}
        <section style={{marginBottom:24}}><div style={{fontFamily:mono,fontSize:10,color:C.green,letterSpacing:"0.15em",marginBottom:8}}>1. EXECUTIVE SUMMARY</div><div style={{background:C.surface,border:`1px solid ${C.border}`,borderLeft:`3px solid ${C.green}`,padding:"16px 20px",borderRadius:"0 3px 3px 0"}}><p style={{fontFamily:sans,fontSize:13,color:C.textSecondary,lineHeight:1.8,margin:0}}>{d.executive}</p></div></section>
        <section style={{marginBottom:24}}><div style={{fontFamily:mono,fontSize:10,color:C.green,letterSpacing:"0.15em",marginBottom:8}}>2. KEY ISSUES</div><table style={{width:"100%",borderCollapse:"collapse"}}><thead><tr style={{borderBottom:`1px solid ${C.border}`}}>{["#","Issue","Severity","Domain"].map(h=>(<th key={h} style={{textAlign:"left",fontFamily:mono,fontSize:9,color:C.textMuted,letterSpacing:"0.1em",padding:"7px 10px"}}>{h}</th>))}</tr></thead><tbody>{d.issues.map((issue,i)=>(<tr key={i} style={{borderBottom:`1px solid ${C.border}`}}><td style={{fontFamily:mono,fontSize:10,color:C.textMuted,padding:"10px"}}>{String(i+1).padStart(2,"0")}</td><td style={{fontFamily:sans,fontSize:12,color:C.textPrimary,padding:"10px"}}>{issue.title}</td><td style={{padding:"10px"}}><SB level={issue.severity}/></td><td style={{padding:"10px"}}><div style={{display:"flex",gap:4,flexWrap:"wrap"}}>{issue.tags.map(t=><Tag key={t} label={t}/>)}</div></td></tr>))}</tbody></table></section>
        <section style={{marginBottom:24}}><div style={{fontFamily:mono,fontSize:10,color:C.green,letterSpacing:"0.15em",marginBottom:8}}>3. RISK ASSESSMENT</div>{d.risks.map((r,i)=>(<div key={i} style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:8,padding:"10px 14px",background:C.surface,border:`1px solid ${C.border}`,borderRadius:3,gap:14,flexWrap:"wrap"}}><span style={{fontFamily:sans,fontSize:13,color:C.textPrimary}}>{r.category}</span><div style={{display:"flex",gap:10,alignItems:"center",flex:1,minWidth:140}}><div style={{flex:1}}><RiskBar score={r.score} color={r.color}/></div><Tag label={r.label} color={r.color} bg={r.color+"18"}/></div></div>))}</section>
        <section style={{marginBottom:24}}><div style={{fontFamily:mono,fontSize:10,color:C.green,letterSpacing:"0.15em",marginBottom:8}}>4. RECOMMENDATIONS</div>{d.recommendations.map((r,i)=>{const pColor=r.priority==="IMMEDIATE"?C.red:r.priority==="SHORT-TERM"?C.amber:r.priority==="MEDIUM-TERM"?C.blue:C.textMuted;return(<div key={i} style={{display:"flex",gap:12,marginBottom:10,alignItems:"flex-start"}}><Tag label={r.priority} color={pColor} bg={pColor+"18"}/><p style={{fontFamily:sans,fontSize:13,color:C.textSecondary,margin:0,lineHeight:1.6,flex:1}}>{r.action}</p></div>);})}</section>
        <div style={{borderTop:`1px solid ${C.border}`,paddingTop:16,display:"flex",justifyContent:"space-between",flexWrap:"wrap",gap:8}}><div style={{fontFamily:mono,fontSize:9,color:C.textMuted}}>POLICY ROOM · DECISION SUPPORT TOOL · COMPLETENESS {d.meta.completeness}%</div><div style={{fontFamily:mono,fontSize:9,color:C.textMuted}}>Built by <span style={{color:C.textSecondary}}>Amirlin Munkhbat</span></div></div>
      </div>
    </div>
  );
}

export default function App(){
  const [view,setView]=useState("landing");
  const [analysis,setAnalysis]=useState(null);
  return(
    <div style={{background:C.bg,minHeight:"100vh",color:C.textPrimary,fontFamily:sans}}>
      <TopBar view={view} setView={setView}/>
      {view==="landing"&&<LandingPage setView={setView} setAnalysis={setAnalysis}/>}
      {view==="upload"&&<UploadRoom setView={setView} setAnalysis={setAnalysis}/>}
      {view==="dashboard"&&<Dashboard data={analysis} setView={setView}/>}
      {view==="brief"&&<BriefingNote data={analysis}/>}
      <style>{`*{box-sizing:border-box;}body{margin:0;}button:hover{opacity:0.88;}@keyframes pulse{0%,100%{opacity:1}50%{opacity:0.3}}@keyframes ticker{from{transform:translateX(0)}to{transform:translateX(-50%)}}::-webkit-scrollbar{width:6px;background:#080c0e;}::-webkit-scrollbar-thumb{background:#1c2a30;border-radius:3px;}`}</style>
    </div>
  );
}
