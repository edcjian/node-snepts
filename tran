const mysql2 = require("mysql2");
const pool = mysql2.createPool({
    host: 'localhost',
    user: 'root',
    password: '123456',
    database: 'aaa',
}).promise()
const transaction = async (callback) => {
    const connection = await pool.getConnection()
    await connection.beginTransaction()
    try {
        await callback(connection)
        await connection.commit()
    } catch (err) {
        await connection.rollback()
        throw err
    } finally {
        connection.release()
    }
}

async function main() {
    await transaction(async (connection) => {
        await connection.query(`insert into test (id, name) VALUE (1, 'test')`)
        // console.log(m.test())
        await connection.query(`insert into test (id, name) VALUE (2, 'kaka')`)
    })
}
main()
