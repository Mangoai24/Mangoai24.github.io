<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Garritas Nails por Ale 🐾</title>

<link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;500;600;700&display=swap" rel="stylesheet">

<style>
:root{
    --crema:#FAF7F2;
    --crema-2:#F2EDE3;
    --verde:#606C38;
    --verde-oscuro:#283618;
    --verde-suave:#89945F;
    --blanco:#FFFFFF;
    --plata:#C0C0C0;
    --plata-claro:#E8E8E8;
    --gris:#EFEFEF;
    --texto:#333333;
    --rojo:#B84A4A;
    --amarillo:#C99A27;
    --whatsapp:#25D366;
}

*{
    box-sizing:border-box;
    margin:0;
    padding:0;
    font-family:'Quicksand',sans-serif;
}

body{
    min-height:100vh;
    background:
        radial-gradient(circle at 10% 10%,rgba(96,108,56,.07) 0 35px,transparent 36px),
        radial-gradient(circle at 90% 85%,rgba(96,108,56,.06) 0 45px,transparent 46px),
        var(--crema);
    color:var(--texto);
    padding:20px;
}

.container{
    width:100%;
    max-width:680px;
    margin:auto;
    background:var(--blanco);
    border:2px solid var(--verde);
    border-radius:24px;
    overflow:hidden;
    box-shadow:0 12px 35px rgba(40,54,24,.12);
}

header{
    background:var(--verde);
    color:white;
    text-align:center;
    padding:27px 20px;
    border-bottom:4px solid var(--plata);
}

.logo-paw{
    font-size:2rem;
    margin-bottom:8px;
}

header h1{
    font-size:1.35rem;
    line-height:1.35;
}

.subtitle{
    margin-top:8px;
    font-size:.82rem;
    opacity:.9;
}

.step{
    display:none;
    padding:25px;
}

.step.active{
    display:block;
}

h2{
    color:var(--verde-oscuro);
    font-size:1.18rem;
    margin-bottom:17px;
    padding-bottom:8px;
    border-bottom:2px solid var(--verde);
}

.section-title{
    color:var(--verde-oscuro);
    font-weight:700;
    margin:18px 0 10px;
}

.service-list{
    display:flex;
    flex-direction:column;
    gap:10px;
}

.service-btn{
    width:100%;
    border:2px solid var(--verde);
    background:var(--crema);
    color:var(--texto);
    border-radius:50px;
    padding:14px 19px;
    display:flex;
    align-items:center;
    justify-content:space-between;
    cursor:pointer;
    font-size:.95rem;
    font-weight:600;
    transition:.2s;
}

.service-btn:hover{
    transform:translateY(-1px);
    box-shadow:0 4px 12px rgba(96,108,56,.15);
}

.service-btn.selected{
    background:var(--verde);
    color:white;
    border-color:var(--verde-oscuro);
}

.service-left{
    display:flex;
    align-items:center;
    gap:8px;
}

.price{
    font-weight:700;
    white-space:nowrap;
}

.info-box{
    background:var(--crema-2);
    border-left:4px solid var(--verde);
    padding:12px 14px;
    border-radius:10px;
    margin:12px 0 18px;
    font-size:.86rem;
    line-height:1.45;
}

.shapes{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:10px;
    margin-bottom:20px;
}

.shape{
    border:2px solid var(--verde);
    background:var(--crema);
    border-radius:16px;
    padding:13px 5px;
    text-align:center;
    cursor:pointer;
    transition:.2s;
}

.shape:hover{
    box-shadow:0 4px 12px rgba(96,108,56,.15);
}

.shape.selected{
    background:var(--verde);
    color:white;
}

.nail{
    width:42px;
    height:60px;
    margin:0 auto 7px;
}

.nail svg{
    width:100%;
    height:100%;
    stroke:currentColor;
    fill:none;
    stroke-width:2.2;
}

.shape-name{
    font-size:.78rem;
    font-weight:700;
}

.extra-row{
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:10px;
    padding:11px 4px;
    border-bottom:1px solid var(--gris);
    font-size:.9rem;
}

.extra-row:last-child{
    border-bottom:none;
}

.number-control{
    width:58px;
    padding:7px;
    border:1px solid var(--verde);
    border-radius:9px;
    text-align:center;
    background:white;
}

.checkbox{
    width:18px;
    height:18px;
    accent-color:var(--verde);
}

.total{
    margin:22px 0 15px;
    padding:17px;
    background:var(--verde-oscuro);
    color:white;
    border-radius:15px;
