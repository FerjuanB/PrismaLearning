~~~
realizar operaciones crud en un async-await 
y utilizar sintaxis como 

~~~
---
Create
---
~~~

    async function main (){
        const newUser = await prisma.user.create({
            data: {
                name: 'Ryan',
                email: 'ryan@email.com'
            }
        })
    }   

~~~


*se nota en el codigo que se llama al metodo prisma luego en el objeto van a salir todos los modelos creados y luego en el modelo elegido hacemos otro punto y saldran todos los metodos para realizar con las tablas, para crear una nueva entrada en la tabla usamos create y con la sintaxis que se ve, ingresamos los datos, que se puede reemplazar sencillamente por unas variables para que reciba los parametros por una query, por ejemplo*

---
Find 
---
~~~


    async function main (){
        const Users = await prisma.user.findMany()
    } 

    main()

~~~

*este metodo sencillo listará todo lo que hay en la tabla user, pero tambien se pueden hacer busquedas por criterios*

---
FindFirst
---
~~~
   async function main (){
        const Users = await prisma.user.findFirst({
            where: {
                id: 2
            }
        })
    }; 
    main();
~~~
*usando el findfirst y luego el where, le estoy dando el criterio de busqueda para que me devuelva el primero que coincida con ese criterio por ej, por id, dentro del where nos aparecera todas las entradas disponibles para ingresar *

__podemos buscar por un valor o por otro:__

~~~
async function main2 (){
        const Users = await prisma.user.findFirst({
            where: {
                OR:[
                    {id:1},
                    {email:"hello@mail.com"}
                ]
            }
        })
    }
    main2()
    
~~~
_cualquiera de los dos, el primero que encuentre, lo va a devolver, si en vez, uso AND, no me va a devolver nada hasta que no haya coincidencia en los dos datos(opera como booleanos)_

---
Delete 
---
~~~
async function deleteUser() {
    const delUser = await prisma.user.delete({
        where:{
            id:1
        }
    }) 
}
~~~
*aqui vemos como se hace un borrado del usuario que coincida con el criterio que esta dentro del where, puede ser cualquier parametro,  y tambien se pueden usar los booleanos*

---
Update
---
~~~
async function updateUser() {
    const updUser = await prisma.user.update({
        where:{
            id:1
        },
        data:{
            lastname: 'Doe'
        }
    }) 
}
~~~
*usar las primary keys para encontrarlo, y luego pasarle por data, dentro de él, el usuario a actualizar.*

---
UpdateMany
--
~~~
async function updateUsers() {
    const updUsers = await prisma.user.update({
        where:{
            name:'Joe'
        },
        data:{
            lastname: 'Dolet'
        }
    }) 
}
~~~
*aca no es necesario el primary key para hacer el update, en el where pasamos e lcriterio a seleccionar para cambiar y en el data ponemos la propiedad y el valor a cambiar, esto devuelve un count, de cuantas coincidencias se cambiaron*