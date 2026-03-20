(async () => {

const token = "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";
const repo = "hanns-luvai-portfolio";

const headers = {
Authorization: `token ${token}`,
"Content-Type": "application/json"
};

// create repo
await fetch("https://api.github.com/user/repos",{
method:"POST",
headers,
body:JSON.stringify({name:repo,private:false})
});

const files = {

"package.json":`
{
"name":"hanns-luvai-portfolio",
"version":"1.0.0",
"private":true,
"scripts":{"dev":"next dev","build":"next build","start":"next start"},
"dependencies":{"next":"13.5.1","react":"18.2.0","react-dom":"18.2.0"}
}
`,

"pages/index.js":`
export default function Home(){
return(
<div style={{fontFamily:"sans-serif",padding:"60px"}}>
<h1>Hanns Luvai</h1>
<p>Professional Land Surveyor in Nairobi, Kenya</p>
<p>Providing land surveying services including boundary identification,
land subdivision and title processing.</p>
</div>
)
}
`,

"pages/profile.js":`
export default function Profile(){
return(
<div style={{padding:"60px"}}>
<h1>Profile</h1>
<p>Hanns Luvai is a professional land surveyor specializing
in cadastral surveys and boundary verification.</p>
</div>
)
}
`,

"pages/works.js":`
export default function Works(){
return(
<div style={{padding:"60px"}}>
<h1>Survey Projects</h1>
<p>Examples of boundary surveys, subdivision planning
and construction layout work.</p>
</div>
)
}
`,

"pages/contact.js":`
export default function Contact(){
return(
<div style={{padding:"60px"}}>
<h1>Contact</h1>
<p>Email: your@email.com</p>
<p>Phone: +254 XXX XXX XXX</p>
<p>Location: Nairobi, Kenya</p>
</div>
)
}
`

};

for (const path in files){

await fetch(
\`https://api.github.com/repos/\${await (await fetch("https://api.github.com/user",{headers})).json().then(u=>u.login)}/\${repo}/contents/\${path}\`,
{
method:"PUT",
headers,
body:JSON.stringify({
message:"initial commit",
content:btoa(files[path])
})
}
);

}

alert("Repository created successfully!");

})();
