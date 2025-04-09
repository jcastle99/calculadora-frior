<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora FRIOR Cambio de Pezoneras</title>
    <!-- Web Monetization (Opcional) -->
    <meta name="monetization" content="$ilp.uphold.com/tu-payment-pointer">
    <!-- Fuentes y Dependencias -->
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script&display=swap" rel="stylesheet">
    <script src="https://js.stripe.com/v3/"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background: #005566;
            color: #333;
        }
        .container {
            max-width: 700px;
            margin: 0 auto;
            background: #fff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            position: relative;
        }
        .logo {
            display: block;
            margin: 0 auto 20px;
            width: 100px;
        }
        h1 {
            text-align: center;
            color: #005566;
            font-size: 24px;
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin: 10px 0 5px;
            font-weight: bold;
            color: #005566;
        }
        input, select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-sizing: border-box;
            font-size: 14px;
        }
        input:focus, select:focus {
            border-color: #005566;
            outline: none;
        }
        button {
            width: 100%;
            padding: 10px;
            background: #005566;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 15px;
            font-size: 14px;
        }
        button:hover {
            background: #003d4a;
        }
        #resultado {
            margin-top: 20px;
            padding: 15px;
            background: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        .modificacion-campos {
            display: none;
            background: #f0f0f0;
            padding: 15px;
            border-radius: 5px;
            margin-top: 10px;
        }
        #whatsapp-section, #donaciones-section, #premium-section {
            display: none;
            margin-top: 20px;
        }
        .signature {
            text-align: center;
            margin-top: 20px;
            font-family: 'Dancing Script', cursive;
            font-size: 28px;
            color: #005566;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
        }
        #premiumButton {
            background: #ff9800;
        }
        #premiumButton:hover {
            background: #e68900;
        }
    </style>
</head>
<body>
    <div class="container">
        <img src="data:image/png;base64,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" alt="Logo FRIOR" class="logo">
        <h1>Calculadora FRIOR Cambio de Pezoneras</h1>
        <form id="formulario">
            <label for="ordenosDia">Ordeños por Día:</label>
            <input type="number" id="ordenosDia" required>

            <label for="puntosOrdeno">Puntos de Ordeño (Inicial):</label>
            <input type="number" id="puntosOrdeno" required>

            <label for="vacas">Vacas Ordeñadas (Inicial):</label>
            <input type="number" id="vacas" required>

            <label for="durabilidad">Durabilidad de Pezoneras por Ordeño por Punto:</label>
            <input type="number" id="durabilidad" value="2500" required>

            <label for="fechaInicio">Fecha de Inicio (opcional):</label>
            <input type="date" id="fechaInicio" placeholder="YYYY-MM-DD">

            <label for="diasEspecificos">Calcular para Días Específicos (opcional):</label>
            <input type="number" id="diasEspecificos" placeholder="Número de días">

            <label for="realizarModificacion">¿Modificar Vacas o Puntos?</label>
            <select id="realizarModificacion" onchange="mostrarCamposModificacion()">
                <option value="no">No</option>
                <option value="si">Sí</option>
            </select>

            <div id="modificacion-campos" class="modificacion-campos">
                <label for="fechaCambio">Fecha de Cambio:</label>
                <input type="date" id="fechaCambio" placeholder="YYYY-MM-DD">

                <label for="nuevoNumeroVacas">Nuevo Número de Vacas:</label>
                <input type="number" id="nuevoNumeroVacas" placeholder="Nuevo número de vacas">

                <label for="nuevoPuntosOrdeno">Nuevo Número de Puntos:</label>
                <input type="number" id="nuevoPuntosOrdeno" placeholder="Nuevo número de puntos">
            </div>

            <button type="button" onclick="calcular()">Calcular</button>
            <button type="button" onclick="limpiarPantalla()">Limpiar</button>
        </form>
        <div id="resultado"></div>

        <!-- Publicidad con Google AdSense -->
        <div style="margin-top: 20px; text-align: center;">
            <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
            <ins class="adsbygoogle"
                 style="display:block"
                 data-ad-client="tu-id-de-cliente"
                 data-ad-slot="tu-id-de-slot"
                 data-ad-format="auto"></ins>
            <script>
                 (adsbygoogle = window.adsbygoogle || []).push({});
            </script>
        </div>

        <!-- WhatsApp Section -->
        <div id="whatsapp-section">
            <label for="codigoCliente">Código del Cliente:</label>
            <input type="text" id="codigoCliente" placeholder="Ingresa el código del cliente" required>
            <button type="button" onclick="enviarWhatsApp()">Enviar por WhatsApp</button>
        </div>

        <!-- Premium Section -->
        <div id="premium-section">
            <button id="premiumButton" onclick="comprarPremium()">Desbloquear Exportación a PDF (5€)</button>
            <div id="premiumContent" style="display: none;">
                <button onclick="exportarPDF()">Exportar a PDF</button>
            </div>
        </div>

        <!-- Donaciones con Ko-fi y Netlify Forms -->
        <div id="donaciones-section" style="text-align: center;">
            <p>¿Te ayudó esta calculadora? ¡Apóyame con un café!</p>
            <a href="https://ko-fi.com/tu-usuario" target="_blank">
                <img src="https://ko-fi.com/img/donate-button.png" alt="Dona en Ko-fi" style="width: 150px;">
            </a>
            <form name="donaciones" method="POST" data-netlify="true" style="margin-top: 20px;">
                <input type="hidden" name="form-name" value="donaciones">
                <label>Deja un mensaje (opcional):</label>
                <textarea name="mensaje"></textarea>
                <button type="submit">Enviar</button>
            </form>
        </div>

        <!-- Marketing de Afiliados -->
        <div style="margin-top: 20px; text-align: center;">
            <p>¿Necesitas pezoneras nuevas? <a href="/comprar-pezoneras" target="_blank">Compra aquí</a> y apoya esta herramienta.</p>
        </div>

        <div class="signature">J.Castle</div>
    </div>

    <script>
        let resultadoTexto = '';
        let costoManoObra = 0;
        let vacasIniciales = 0;
        let puntosOrdenoIniciales = 0;
        const stripe = Stripe('tu-clave-publica-de-stripe'); // Reemplaza con tu clave pública de Stripe

        function mostrarCamposModificacion() {
            const seleccion = document.getElementById('realizarModificacion').value;
            document.getElementById('modificacion-campos').style.display = seleccion === 'si' ? 'block' : 'none';
        }

        function calcular() {
            const ordenosDia = parseInt(document.getElementById('ordenosDia').value) || 0;
            let puntosOrdeno = parseInt(document.getElementById('puntosOrdeno').value) || 0;
            const vacas = parseInt(document.getElementById('vacas').value) || 0;
            const durabilidad = parseInt(document.getElementById('durabilidad').value) || 0;
            const fechaInicioInput = document.getElementById('fechaInicio').value;
            const diasEspecificos = parseInt(document.getElementById('diasEspecificos').value) || 0;
            const realizarModificacion = document.getElementById('realizarModificacion').value;
            const fechaCambioInput = document.getElementById('fechaCambio').value;
            const nuevoNumeroVacas = parseInt(document.getElementById('nuevoNumeroVacas').value) || 0;
            const nuevoPuntosOrdeno = parseInt(document.getElementById('nuevoPuntosOrdeno').value) || 0;

            vacasIniciales = vacas;
            puntosOrdenoIniciales = puntosOrdeno;

            let fechaInicio = fechaInicioInput ? new Date(fechaInicioInput) : new Date();

            if (diasEspecificos > 0 && !ordenosDia && !puntosOrdeno && !vacas) {
                const fechaDiasEspecificos = new Date(fechaInicio.getTime() + diasEspecificos * 86400000);
                resultadoTexto = `
                    Calculadora FRIOR Cambio de Pezoneras
                    Fecha Inicio: ${fechaInicio.toLocaleDateString('es-ES')}
                    Fecha para ${diasEspecificos} Días: ${fechaDiasEspecificos.toLocaleDateString('es-ES')}
                `;
                mostrarResultados();
                return;
            }

            if (!ordenosDia || !puntosOrdeno || !vacas || !durabilidad) {
                alert("Completa todos los campos requeridos para el cálculo completo.");
                return;
            }

            const ordeñosTotalesPorDia = ordenosDia * vacas;
            const ordeñosPorPuntoPorDia = ordeñosTotalesPorDia / puntosOrdeno;
            const diasDurabilidadInicial = durabilidad / ordeñosPorPuntoPorDia;

            const fechaProximoCambioInicial = new Date(fechaInicio);
            fechaProximoCambioInicial.setDate(fechaInicio.getDate() + Math.floor(diasDurabilidadInicial));

            let fechaDiasEspecificos = diasEspecificos > 0 ? `Fecha para ${diasEspecificos} Días: ${new Date(fechaInicio.getTime() + diasEspecificos * 86400000).toLocaleDateString('es-ES')}` : '';

            const diasEnMes = 30.42;
            const mesesEquivalentes = Math.round(diasDurabilidadInicial / diasEnMes);

            const pezonerasPorPunto = 4;
            let totalPezoneras = puntosOrdeno * pezonerasPorPunto;
            costoManoObra = puntosOrdeno * 4;
            let desgastePezonerasPorDiaInicial = totalPezoneras / diasDurabilidadInicial;

            let durabilidadAjustada = diasDurabilidadInicial;
            let fechaProximoCambioAjustada = fechaProximoCambioInicial;
            let desgastePezonerasPorDiaAjustada = desgastePezonerasPorDiaInicial;
            let mensajeAjuste = '';

            if (realizarModificacion === 'si' && fechaCambioInput && (nuevoNumeroVacas > 0 || nuevoPuntosOrdeno > 0)) {
                const fechaCambio = new Date(fechaCambioInput);
                const diasTranscurridos = Math.floor((fechaCambio - fechaInicio) / (1000 * 60 * 60 * 24));

                if (diasTranscurridos < 0) {
                    alert("La fecha de cambio no puede ser anterior a la fecha de inicio.");
                    return;
                }

                const ordeñosPorPuntoHastaCambio = ordeñosPorPuntoPorDia * diasTranscurridos;
                const durabilidadRestante = durabilidad - ordeñosPorPuntoHastaCambio;

                if (durabilidadRestante <= 0) {
                    mensajeAjuste = `Nota: Las pezoneras ya debieron cambiarse antes de ${fechaCambio.toLocaleDateString('es-ES')}.`;
                } else {
                    const vacasAjustadas = nuevoNumeroVacas > 0 ? nuevoNumeroVacas : vacas;
                    const puntosOrdenoAjustados = nuevoPuntosOrdeno > 0 ? nuevoPuntosOrdeno : puntosOrdeno;
                    totalPezoneras = puntosOrdenoAjustados * pezonerasPorPunto;
                    costoManoObra = puntosOrdenoAjustados * 4;
                    const nuevosOrdeñosTotalesPorDia = ordenosDia * vacasAjustadas;
                    const nuevosOrdeñosPorPuntoPorDia = nuevosOrdeñosTotalesPorDia / puntosOrdenoAjustados;
                    const diasDurabilidadRestante = durabilidadRestante / nuevosOrdeñosPorPuntoPorDia;

                    fechaProximoCambioAjustada = new Date(fechaCambio);
                    fechaProximoCambioAjustada.setDate(fechaCambio.getDate() + Math.floor(diasDurabilidadRestante));

                    durabilidadAjustada = diasTranscurridos + diasDurabilidadRestante;
                    desgastePezonerasPorDiaAjustada = totalPezoneras / durabilidadAjustada;

                    mensajeAjuste = `
                        Ajuste por Modificación:
                        Fecha de Cambio: ${fechaCambio.toLocaleDateString('es-ES')}
                        Nuevo Número de Vacas: ${vacasAjustadas}
                        Nuevo Número de Puntos: ${puntosOrdenoAjustados}
                        Durabilidad Ajustada: ${Math.floor(durabilidadAjustada)} días
                        Nueva Fecha de Cambio: ${fechaProximoCambioAjustada.toLocaleDateString('es-ES')}
                        Total Pezoneras: ${totalPezoneras}
                        Desgaste por Día: ${desgastePezonerasPorDiaAjustada.toFixed(2)}
                    `;
                }
            }

            resultadoTexto = `
                Calculadora FRIOR Cambio de Pezoneras
                Fecha Inicio: ${fechaInicio.toLocaleDateString('es-ES')}
                Vacas Iniciales: ${vacasIniciales}
                Puntos Iniciales: ${puntosOrdenoIniciales}
                Durabilidad Inicial: ${Math.floor(diasDurabilidadInicial)} días
                Próximo Cambio Inicial: ${fechaProximoCambioInicial.toLocaleDateString('es-ES')}
                Meses Equivalentes: ${mesesEquivalentes}
                ${fechaDiasEspecificos}
                Total Pezoneras Inicial: ${puntosOrdeno * pezonerasPorPunto}
                Desgaste por Día Inicial: ${desgastePezonerasPorDiaInicial.toFixed(2)}
                Costo Mano de Obra: ${costoManoObra} €
                ${mensajeAjuste}
            `;
            mostrarResultados();
        }

        function mostrarResultados() {
            document.getElementById('resultado').innerHTML = resultadoTexto.replace(/\n/g, '<br>');
            document.getElementById('whatsapp-section').style.display = 'block';
            document.getElementById('premium-section').style.display = 'block';
            document.getElementById('donaciones-section').style.display = 'block';
        }

        function enviarWhatsApp() {
            const codigoCliente = document.getElementById('codigoCliente').value.trim();
            if (!codigoCliente) {
                alert("Ingresa el código del cliente.");
                return;
            }
            const mensajeWhatsApp = `Código del Cliente: ${codigoCliente}\n${resultadoTexto}`;
            const urlWhatsApp = `https://api.whatsapp.com/send?text=${encodeURIComponent(mensajeWhatsApp)}`;
            window.open(urlWhatsApp, '_blank');
        }

        async function comprarPremium() {
            try {
                const response = await fetch('/.netlify/functions/premium', {
                    method: 'POST',
                    body: JSON.stringify({ token: 'tok_visa' }), // En producción, usa Stripe Elements para obtener un token real
                });
                const data = await response.json();
                if (data.success) {
                    document.getElementById('premiumContent').style.display = 'block';
                    alert('¡Acceso Premium desbloqueado!');
                } else {
                    alert('Error al procesar el pago.');
                }
            } catch (error) {
                alert('Error: ' + error.message);
            }
        }

        function exportarPDF() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            doc.text(document.getElementById('resultado').innerText, 10, 10);
            doc.save('resultado_calculadora.pdf');
        }

        function limpiarPantalla() {
            const durabilidad = document.getElementById('durabilidad').value;
            document.getElementById('formulario').reset();
            document.getElementById('durabilidad').value = durabilidad;
            document.getElementById('modificacion-campos').style.display = 'none';
            document.getElementById('resultado').innerHTML = '';
            document.getElementById('whatsapp-section').style.display = 'none';
            document.getElementById('premium-section').style.display = 'none';
            document.getElementById('donaciones-section').style.display = 'none';
            document.getElementById('codigoCliente').value = '';
            resultadoTexto = '';
            costoManoObra = 0;
            vacasIniciales = 0;
            puntosOrdenoIniciales = 0;
        }

        document.querySelectorAll('#formulario input').forEach(input => {
            input.addEventListener('keydown', function(event) {
                if (event.key === 'Enter') {
                    event.preventDefault();
                    calcular();
                }
            });
        });
    </script>
</body>
</html>
