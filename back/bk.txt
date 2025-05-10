import express from 'express';
import pkg from '@prisma/client';
import cors from 'cors';
const { PrismaClient } = pkg;

const prisma = new PrismaClient();
const app = express();
app.use(express.json());
app.use(cors());

app.get('/usuarios', async (req, res) => {
    const users = await prisma.user.findMany()
    res.status(200).json(users)
});

app.post('/usuarios', async (req, res) => {

    await prisma.user.create({
        data: {
            name: req.body.name,
            email: req.body.email,
            age: req.body.age       
        }
    })
    res.status(201).json(req.body);
});

app.listen(3000, () => {
    console.log('Servidor rodando na porta 3000');
});