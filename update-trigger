CREATE OR REPLACE TRIGGER bb_reorder_trg
   AFTER UPDATE OF stock ON bb_product
   FOR EACH ROW 
DECLARE
  v_onorder_num NUMBER(4);
 BEGIN
  If :NEW.stock <= :NEW.reorder THEN
   SELECT SUM(qty)
    INTO v_onorder_num
    FROM bb_product_request
    WHERE idProduct = :NEW.idProduct
     AND dtRecd IS NULL;
   IF v_onorder_num IS NULL THEN v_onorder_num := 0; END IF;
   IF v_onorder_num = 0 THEN
     INSERT INTO bb_product_request (idRequest, idProduct, dtRequest, qty)
       VALUES (bb_prodreq_seq.NEXTVAL, :NEW.idProduct, SYSDATE, :NEW.reorder);
   END IF;
  END IF;
END;
