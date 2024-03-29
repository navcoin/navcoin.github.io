.. _serialization:

Serialization
=============


.. _header_s:

Block Header
------------

================ ===================== ======================  ====================
Field            Type                  Length                  Present
================ ===================== ======================  ====================
nVersion         signed int            4 bytes                 Always
hashPrevBlock    uint256               32 bytes                Always
hashMerkleRoot   uint256               32 bytes                Always
nTime            unsigned int          4 bytes                 Always
nBits            unsigned int          4 bytes                 Always
nNonce           unsigned int          4 bytes                 Always
================ ===================== ======================  ====================

Block
-----

================ ===================== ======================  ====================
Field            Type                  Length                  Present
================ ===================== ======================  ====================
blockHeader      :ref:`header_s`       70 bytes                Always
vTx              :ref:`tx_s` vector    Variable                Always
================ ===================== ======================  ====================

.. _bp_s:

Bulletproof Range Proof
-----------------------

================ ===================== ======================  ======================
Field            Type                  Length                  Present
================ ===================== ======================  ======================
V                :ref:`g1_s` vector    Variable                Always
L                :ref:`g1_s` vector    Variable                Always
R                :ref:`g1_s` vector    Variable                Always
A                :ref:`g1_s`                                   Always
S                :ref:`g1_s`                                   Always
T1               :ref:`g1_s`                                   Always
T2               :ref:`g1_s`                                   Always
taux             :ref:`sca_s`                                  Always
mu               :ref:`sca_s`                                  Always
a                :ref:`sca_s`                                  Always
b                :ref:`sca_s`                                  Always
t                :ref:`sca_s`                                  Always
================ ===================== ======================  ======================


.. _tx_s:

Transaction
-----------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
nVersion         signed int             4 bytes                 Always
vin              :ref:`tx_in_s` vector  Variable                Always
flags            unsigned char          1 byte                  If vin.size() == 0
vin              :ref:`tx_in_s` vector  Variable                If vin.size() == 0
vout             :ref:`tx_out_s` vector Variable                Always
wit              :ref:`tx_wit_s` vector Same as vin             If flags&1
nLockTime        unsigned int           4 bytes                 Always
vchTxSig         :ref:`g2_s`                                    If nVersion & 0x20
================ ====================== ======================  ======================

.. _tx_in_s:

Transaction Input
-----------------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
prevout          :ref:`outpoint_s`      36 bytes                Always
scriptSig        unsigned char vector   Variable                Always
nSequence        unsigned int           4 bytes                 Always
================ ====================== ======================  ======================

.. _tx_out_s:

Transaction Output
------------------

================ ====================== ======================  =========================
Field            Type                   Length                  Present
================ ====================== ======================  =========================
nValue           signed int             8 bytes                 Always
nFlags           unsigned int           8 bytes                 If nValue == INT64_MAX
scriptPubKey     unsigned char vector   Variable                Always
rangeProof       :ref:`bp_s`                                    If nFlags & 0x01
spendingKey      :ref:`g1_s`            48 bytes                If nFlags & 0x01
blindingKey      :ref:`g1_s`            48 bytes                If nFlags & 0x01
ephemeralKey     :ref:`g1_s`            48 bytes                If nFlags & 0x01
viewTag          unsigned int           2 bytes                 If nFlags & 0x01
tokenId          :ref:`token_id_s`                              If nFlags & 0x02
================ ====================== ======================  =========================

.. _sca_s:

Scalar
------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
data             Scalar                 32                      Always
================ ====================== ======================  ======================

.. _g1_s:

G1Element
---------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
data             G1Element              48                      Always
================ ====================== ======================  ======================

.. _g2_s:

G2Element
---------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
data             G2Element              96                      Always
================ ====================== ======================  ======================


.. _token_id_s:

TokenId
---------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
tokenId          uint256                32                      Always
nftId            unsigned int           8                       Always
================ ====================== ======================  ======================


.. _outpoint_s:

OutPoint
--------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
hash             uint256                32                      Always
n                unsigned int           4                       Always
================ ====================== ======================  ======================

.. _tx_wit_s:

TxWitness
---------

================ =============================== ======================  ======================
Field            Type                            Length                  Present
================ =============================== ======================  ======================
stack            vector of unsigned char vectors Variable                Always
================ =============================== ======================  ======================
