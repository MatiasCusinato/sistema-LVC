<script>
export default {
    methods: {
        funcObtenerDatosPorId(ruta, id) {
            let urlDestino = "http://127.0.0.1:8000/api/" + ruta + "/" + id
            console.log(urlDestino)
            return fetch(urlDestino,
            {
                method: 'GET',
                headers: {
                    'Content-Type': 'application/json'
                },
            })
            .then(res => {
                return res.json()
                }
            )
            .catch(err => console.log('error fetch:', err))
        },
        funcObtenerDatos(ruta) {
            let urlDestino = "http://127.0.0.1:8000/api/" + ruta 
            return fetch(urlDestino,
            {
                method: 'GET',
                headers: {
                    'Content-Type': 'application/json'
                },
            })
            .then(res => {
                return res.json()
                }
            )
            .catch(err => console.log('Error fetch:', err))
        },
        funcInsertarDatos(ruta, datosIngresar) {
            let urlDestino = "http://127.0.0.1:8000/api/" + ruta 
            return fetch(urlDestino,
            {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(datosIngresar)
            })
            .then(res => {
                return res.json()
                }
            )
            .catch(err => console.log('Error fetch:', err))
        },
        funcEditarDatos(ruta, id, datosIngresar) {
            let urlDestino = "http://127.0.0.1:8000/api/" + ruta + "/" + id
            return fetch(urlDestino,
            {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(datosIngresar)
            })
            .then(res => {
                return res.json()
                }
            )
            .catch(err => console.log('Error fetch:', err))
        },
        funcEliminarDatos(ruta, id) {
            let urlDestino = "http://127.0.0.1:8000/api/" + ruta + "/" + id
            return fetch(urlDestino,
            {
                method: 'DELETE',
                headers: {
                    'Content-Type': 'application/json'
                },
            })
            .catch(err => console.log('Error fetch:', err))
        },
    }
}
</script>