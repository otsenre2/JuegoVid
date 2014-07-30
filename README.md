JuegoVid
========

<!DOCTYPE html>
<head>

<title>Juego de la vida</title>
<link rel="stylesheet" href="estilos.css">
</head>
<script type="text/javascript"> 

function CambiarFondo(celula) { 
	if (celula.style.backgroundColor == "black") { 
		celula.style.backgroundColor = "white"; }
	else { 
		celula.style.backgroundColor = "black"; 
	} 
} 
function ImprimirRed() { 
	var red=new Array(50);
	for (i = 0; i < 50; i++){
		red[i]=new Array(50);
	}
	for (i=0; i<50; i++){
		for (e=0; e<50; e++){

			red[i][e] = "<td id='i"+i+"e"+e+"' onclick='CambiarFondo(this)'></td>";
		}
	}
	for (i=0; i<50; i++){
		document.write("<tr>");
		for (e=0; e<50; e++){
			document.write(red[i][e]);
		}
		document.write("</tr>");
	}
}
function GuardarRed() { 
	var RedIni=new Array(50);
	for (i = 0; i < 50; i++){
		RedIni[i]=new Array(50);
	}
	for (i=0; i<50; i++){
		for (e=0; e<50; e++){
			cel=document.getElementById("i"+i+"e"+e);
			if (cel.style.backgroundColor == "black"){
				RedIni[i][e]=1;
			}else{
				RedIni[i][e]=0;
			}
		}
	}
	return RedIni;
}
function Aura(RedAura){
	for (i=0; i<50; i++){
		for (e=0; e<50; e++){
			if (RedAura[i][e]==1){
				if (i!=0){if (RedAura[i-1][e]!=1){RedAura[i-1][e]=2;}}
				if (i!=0 && e!=49){if (RedAura[i-1][e+1]!=1){RedAura[i-1][e+1]=2;}}
				if (e!=49){if (RedAura[i][e+1]!=1){RedAura[i][e+1]=2;}}
				if (i!=49 && e!=49){if (RedAura[i+1][e+1]!=1){RedAura[i+1][e+1]=2;}}
				if (i!=49){if (RedAura[i+1][e]!=1){RedAura[i+1][e]=2;}}
				if (i!=49 && e!=0){if (RedAura[i+1][e-1]!=1){RedAura[i+1][e-1]=2;}}
				if (e!=0){if (RedAura[i][e-1]!=1){RedAura[i][e-1]=2;}}
				if (i!=0 && e!=0){if (RedAura[i-1][e-1]!=1){RedAura[i-1][e-1]=2;}}
			}
		}
	}
	return RedAura;
}
function Mueren(RedMue){
	var RedViva=new Array(50);
	for (i = 0; i < 50; i++){
		RedViva[i]=new Array(50);
	}
	for (i=0; i<50; i++){
		for (e=0; e<50; e++){
			if (RedMue[i][e]==1){
				cel=0;
				if (i!=0){if (RedMue[i-1][e]==1){cel++;}}
				if (i!=0 && e!=49){if (RedMue[i-1][e+1]===1){cel++;}}
				if (e!=49){if (RedMue[i][e+1]==1){cel++;}}
				if (i!=49 && e!=49){if (RedMue[i+1][e+1]==1){cel++;}}
				if (i!=49){if (RedMue[i+1][e]==1){cel++;}}
				if (i!=49 && e!=0){if (RedMue[i+1][e-1]==1){cel++;}}
				if (e!=0){if (RedMue[i][e-1]==1){cel++;}}
				if (i!=0 && e!=0){if (RedMue[i-1][e-1]==1){cel++;}}
			}
			if (cel==2 || cel==3){RedViva[i][e]=1;cel=0;}
			else {RedViva[i][e]=0;}
		}
	}
	return RedViva;
}
function Nacen(RedMue){
	var RedNace=new Array(50);
	for (i = 0; i < 50; i++){
		RedNace[i]=new Array(50);
	}
	for (i=0; i<50; i++){
		for (e=0; e<50; e++){
			if (RedMue[i][e]==2){
				cel=0;
				if (i!=0){if (RedMue[i-1][e]==1){cel++;}}
				if (i!=0 && e!=49){if (RedMue[i-1][e+1]===1){cel++;}}
				if (e!=49){if (RedMue[i][e+1]==1){cel++;}}
				if (i!=49 && e!=49){if (RedMue[i+1][e+1]==1){cel++;}}
				if (i!=49){if (RedMue[i+1][e]==1){cel++;}}
				if (i!=49 && e!=0){if (RedMue[i+1][e-1]==1){cel++;}}
				if (e!=0){if (RedMue[i][e-1]==1){cel++;}}
				if (i!=0 && e!=0){if (RedMue[i-1][e-1]==1){cel++;}}
			}
			if (cel==3){RedNace[i][e]=1;cel=0;}
			else {RedNace[i][e]=0;}
		}
	}
	return RedNace;
}
function JuegoVida(){
	var NuevaRed=new Array(50);
	for (i = 0; i < 50; i++){
		NuevaRed[i]=new Array(50);
	}
	AuraRed=Aura(GuardarRed());
	MuerenRed=Mueren(AuraRed);
	NacenRed=Nacen(AuraRed);
	for (i=0; i<50; i++){
		for (e=0; e<50; e++){
			NuevaRed[i][e]=MuerenRed[i][e]+NacenRed[i][e];
		}
	}
	return NuevaRed;
}
function VerRed(NuevaRed){
	for (i=0; i<50; i++){
		for (e=0; e<50; e++){
			cel=document.getElementById("i"+i+"e"+e)
			if (NuevaRed[i][e] == 1){
				cel.style.backgroundColor = "black";
			}else{
				cel.style.backgroundColor = "white";
			}
		}
	}
}
function tiempo() { 
setTimeout ("VerRed(JuegoVida());tiempo();", 300);
}
</script> 
<body>
<h1>
Juego de la Vida
</h1 >
<input type="button" id="comiezo" value="Comenzar" onclick="tiempo()">

<table>
<script type="text/javascript">ImprimirRed();</script>
</table>


</body>

</html>

=================================================================================
Hoja de estilos

body {
  padding-left: 1em;
  font-family: Georgia, "Times New Roman",
        Times, serif;
  color: purple;
  background-color: #d8da3d;
  text-align: center;
    }

h1{
text-align: center;
}
td{
width:10px;
height:10px;
background-color: #FFFFFF
}





